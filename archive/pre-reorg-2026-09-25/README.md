# Archived 2026-09-25 — reorg cleanup

Everything here was pulled out of the main project tree during a reorganization pass, per
Anthony's direction: keep it (don't delete — the brand and app are both still active work,
so nothing gets thrown away yet), but get it out of the way of the real structure
(`documents/`, `brand/`, `assets/`, `supabase/`, `app/`).

| Folder/file | What it is | Why it's here |
|---|---|---|
| `news-template-wagtail-boilerplate/` | A Django/Wagtail CMS boilerplate ("news template") | Completely different tech stack, unrelated to this project — looks like it was dropped in from somewhere else |
| `digital-allies-design-system/` | Digital Allies' own brand/design system | Wrong client — this project is HCTC-only |
| `cms-templates/` | Generic CMS page templates mentioning "Digital Allies" | Wrong client, and not referenced anywhere in this project's code |
| `caladrius-brand-review.html` | A brand review for "Caladrius" | Unrelated brand/client entirely |
| `healthcare-training-center-full-make-export.make` | The raw 37MB "Make" platform export | Superseded by the real code in `app/` and `src/` |
| `design-system-bundle-incomplete-duplicate/` | A near-duplicate of `public/_ds/healthcare-training-center-design-system/` | Missing the Phosphor-Fill font file; the complete version was kept in place at `public/_ds/` |
| `figma-learner-app-export/` | The original Figma/Make learner-app HTML+JSX export (3x-duplicated source inside it) | Superseded by the real, hand-built app in `app/`. Its design-handoff spec was extracted first — see `documents/learner-app-design-handoff-reference.md` |
| `stale-review-index/` | The old `review/` folder | Every README in it linked to paths that no longer exist (`hctc-backup/`, old `html docs/` location, etc.) — dead scaffolding from before the 2026-09-20 move out of `da-platform` |
| `unfilled-make-guidelines-placeholders/` | The old `guidelines/` folder | Generic, never-customized "Make" template placeholders (literal `<PACKAGE_NAME>` tokens, "Add your own guidelines here") |
| `vite-boilerplate-unused/` | `react.svg`, `vite.svg` | Stock `npm create vite` scaffold logos, confirmed unused anywhere in `app/src` |
| `stale-VERCEL_SETUP.md` | Old deployment doc | Described the root `index.html` as a redirect to a Learner-App HTML file — no longer true, the root is now the design-system Vite app and `app/` is the real one |
| `supabase-zips/` | `supabase.zip`, `utils.zip` | Zipped copies of files that already exist unzipped elsewhere in the project (`functions/server/*`, `supabase/info.tsx`) |
| `design-export-html-snapshots/` | 9 sequential "code copy N.html" files | Iterative design-export snapshots, superseded by real code |

Nothing here is imported or referenced by either live app (`app/` or the root design-system app) — verified by building both after this archive pass.
