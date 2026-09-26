## 3. DATABASE SCHEMA (Detailed)

### Users & Authentication
```sql
-- Supabase auth_users (managed by Supabase)
-- Extended user profile
CREATE TABLE users (
  id UUID PRIMARY KEY REFERENCES auth.users(id),
  email TEXT UNIQUE NOT NULL,
  display_name TEXT,
  role TEXT CHECK (role IN ('admin', 'learner', 'manager', 'auditor')),
  tech_comfort_level INT (1-10 from form),
  created_at TIMESTAMP DEFAULT NOW(),
  last_login TIMESTAMP,
  is_active BOOLEAN DEFAULT TRUE
);

-- Role-based access control
CREATE TABLE user_roles (
  id UUID PRIMARY KEY,
  user_id UUID REFERENCES users(id),
  role TEXT,
  granted_by UUID REFERENCES users(id),
  created_at TIMESTAMP DEFAULT NOW()
);
```

### Courses & Content
```sql
CREATE TABLE courses (
  id UUID PRIMARY KEY,
  title TEXT NOT NULL,
  description TEXT,
  content_status TEXT CHECK (content_status IN ('draft', 'published', 'archived')),
  created_by UUID REFERENCES users(id),
  created_at TIMESTAMP DEFAULT NOW(),
  updated_at TIMESTAMP DEFAULT NOW(),
  is_published BOOLEAN DEFAULT FALSE
);

CREATE TABLE lessons (
  id UUID PRIMARY KEY,
  course_id UUID REFERENCES courses(id),
  title TEXT NOT NULL,
  lesson_order INT,
  video_url TEXT, -- Vimeo embed or AWS S3 signed URL
  transcript TEXT, -- For accessibility
  duration_minutes INT,
  created_at TIMESTAMP DEFAULT NOW()
);

CREATE TABLE content_blocks (
  id UUID PRIMARY KEY,
  lesson_id UUID REFERENCES lessons(id),
  block_type TEXT CHECK (block_type IN ('text', 'image', 'callout', 'quote', 'list')),
  content TEXT,
  block_order INT,
  created_at TIMESTAMP DEFAULT NOW()
);
```

### Quizzes & Assessments
```sql
CREATE TABLE quizzes (
  id UUID PRIMARY KEY,
  lesson_id UUID REFERENCES lessons(id),
  passing_score INT DEFAULT 70,
  attempts_allowed INT DEFAULT 3,
  time_limit_minutes INT,
  created_at TIMESTAMP DEFAULT NOW()
);

CREATE TABLE quiz_questions (
  id UUID PRIMARY KEY,
  quiz_id UUID REFERENCES quizzes(id),
  question_text TEXT NOT NULL,
  question_type TEXT CHECK (question_type IN ('multiple_choice', 'true_false', 'short_answer')),
  question_order INT,
  created_at TIMESTAMP DEFAULT NOW()
);

CREATE TABLE quiz_options (
  id UUID PRIMARY KEY,
  question_id UUID REFERENCES quiz_questions(id),
  option_text TEXT NOT NULL,
  is_correct BOOLEAN DEFAULT FALSE,
  option_order INT
);

CREATE TABLE quiz_responses (
  id UUID PRIMARY KEY,
  user_id UUID REFERENCES users(id),
  quiz_id UUID REFERENCES quizzes(id),
  attempted_at TIMESTAMP DEFAULT NOW(),
  score INT,
  passed BOOLEAN,
  time_spent_minutes INT
);

CREATE TABLE question_responses (
  id UUID PRIMARY KEY,
  quiz_response_id UUID REFERENCES quiz_responses(id),
  question_id UUID REFERENCES quiz_questions(id),
  user_answer TEXT,
  is_correct BOOLEAN
);
```

### Progress & Certificates
```sql
CREATE TABLE course_progress (
  id UUID PRIMARY KEY,
  user_id UUID REFERENCES users(id),
  course_id UUID REFERENCES courses(id),
  started_at TIMESTAMP DEFAULT NOW(),
  last_accessed_at TIMESTAMP,
  completion_percentage INT DEFAULT 0,
  completed_at TIMESTAMP,
  UNIQUE(user_id, course_id)
);

CREATE TABLE lesson_progress (
  id UUID PRIMARY KEY,
  user_id UUID REFERENCES users(id),
  lesson_id UUID REFERENCES lessons(id),
  started_at TIMESTAMP DEFAULT NOW(),
  completed_at TIMESTAMP,
  UNIQUE(user_id, lesson_id)
);

CREATE TABLE certificates (
  id UUID PRIMARY KEY,
  user_id UUID REFERENCES users(id),
  course_id UUID REFERENCES courses(id),
  issued_at TIMESTAMP DEFAULT NOW(),
  pdf_url TEXT,
  verification_code TEXT UNIQUE, -- For verification endpoint
  is_revoked BOOLEAN DEFAULT FALSE,
  revoked_at TIMESTAMP
);
```

### HIPAA Compliance & Auditing
```sql
-- Audit log: every action logged
CREATE TABLE audit_logs (
  id UUID PRIMARY KEY,
  user_id UUID REFERENCES users(id),
  action TEXT NOT NULL, -- 'CREATE', 'UPDATE', 'DELETE', 'LOGIN', 'DOWNLOAD'
  table_name TEXT,
  record_id UUID,
  old_values JSONB, -- Previous state
  new_values JSONB, -- New state
  ip_address INET,
  user_agent TEXT,
  created_at TIMESTAMP DEFAULT NOW()
);

-- Data retention policy
CREATE TABLE data_retention_policies (
  id UUID PRIMARY KEY,
  data_type TEXT, -- 'course_completion', 'quiz_results', 'audit_logs'
  retention_years INT DEFAULT 7,
  deletion_schedule TEXT, -- 'automatic' or 'manual'
  created_at TIMESTAMP DEFAULT NOW()
);

-- Breach notification log
CREATE TABLE breach_incidents (
  id UUID PRIMARY KEY,
  detected_at TIMESTAMP,
  description TEXT,
  affected_users INT,
  notification_sent_at TIMESTAMP,
  investigation_complete BOOLEAN DEFAULT FALSE,
  created_at TIMESTAMP DEFAULT NOW()
);
```

### Billing & Subscriptions
```sql
CREATE TABLE subscription_plans (
  id UUID PRIMARY KEY,
  name TEXT, -- 'Individual', 'Organization', 'Enterprise'
  price_per_month_cents INT,
  max_learners INT,
  features JSONB, -- What's included
  created_at TIMESTAMP DEFAULT NOW()
);

CREATE TABLE subscriptions (
  id UUID PRIMARY KEY,
  customer_id UUID REFERENCES users(id),
  plan_id UUID REFERENCES subscription_plans(id),
  stripe_subscription_id TEXT,
  status TEXT CHECK (status IN ('active', 'paused', 'cancelled')),
  started_at TIMESTAMP,
  ended_at TIMESTAMP,
  renewal_date TIMESTAMP,
  created_at TIMESTAMP DEFAULT NOW()
);

CREATE TABLE invoices (
  id UUID PRIMARY KEY,
  subscription_id UUID REFERENCES subscriptions(id),
  stripe_invoice_id TEXT,
  amount_cents INT,
  status TEXT CHECK (status IN ('draft', 'sent', 'paid', 'failed')),
  issued_at TIMESTAMP,
  paid_at TIMESTAMP,
  created_at TIMESTAMP DEFAULT NOW()
);
```

### Row-Level Security (RLS) Policies
```sql
-- Learners can only see their own progress
CREATE POLICY learner_progress_isolation ON course_progress
  USING (user_id = auth.uid());

-- Admins can see all progress
CREATE POLICY admin_see_all ON course_progress
  USING (auth.jwt() ->> 'role' = 'admin');

-- Quiz responses only visible to learner + admins
CREATE POLICY quiz_response_isolation ON quiz_responses
  USING (user_id = auth.uid() OR auth.jwt() ->> 'role' = 'admin');
```

---

