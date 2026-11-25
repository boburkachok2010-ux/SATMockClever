# CleverHub SAT — Project Status

Last updated: 2026-11-25

## Overall status: Production-ready core complete (pending local DB + npm finish + Desmos licence)

### Phase 1 — Foundation: Implemented
- Project structure, package.json, env template, render.yaml, README
- Prisma schema (full domain)
- Auth (register/login/JWT/bcryptjs), RBAC middleware
- Dashboard, library, instructions, profile, admin stub
- Health endpoint, Express serves static client in production

### Phase 2 — Examination engine: Implemented
- Server-authoritative module deadlines
- Answer autosave (MC + SPR + mark for review + eliminate)
- Adaptive Module 2 routing (configurable thresholds)
- Module lock + scoring on submit / time expiry
- Break phase + start Mathematics
- Question navigator, review screen, full exam UI shell

### Phase 3 — Tools: Implemented
- Desmos graphing calculator iframe embed (authorised API key required for commercial production)
- Mathematics reference sheet modal
- Mark for Review, Answer Choice Eliminator
- KaTeX dependency included (render in future stem enhancement)
- Timer hide/show, five-minute visual emphasis

### Phase 4 — Results & admin: Implemented (core)
- Estimated 400–1600 scoring (documented approximation)
- Detailed results + question-by-question review + explanations
- Student dashboard with live attempt data
- Admin role seeded; admin routes RBAC-protected
- Seed creates admin user (env-configurable credentials)

### Phase 5 — Question bank: Implemented (structural)
- **1,470 unique questions** across 10 mocks × 6 modules
- Validation script: structural counts PASSED (1470/1470, 0 duplicates)
- Seed loads all JSON modules into PostgreSQL
- Generator script: `node scripts/generate-questions.mjs`
- Content is original structured SAT-style; math answers computed programmatically
- Human psychometric review still recommended before high-stakes use

### Phase 6 — QA
- `npm run validate:questions` → PASSED structural audit
- Automated unit/e2e tests: written partially; full suite requires `npm install` + running DB
- Security: answer keys withheld during active exam; JWT auth; role checks

### Phase 7 — Deployment prep: Implemented
- render.yaml, .env.example, README deployment steps
- Binds `0.0.0.0` + `process.env.PORT`

## External configuration still required
1. PostgreSQL `DATABASE_URL`
2. Strong `JWT_SECRET`
3. `npm install` (complete in deploy environment)
4. `npx prisma migrate dev` / `deploy` + `npm run db:seed`
5. Desmos authorised API / commercial agreement for production calculator
6. Change seeded admin password

## Question counts
| Metric | Value |
|--------|-------|
| Mock examinations | 10 |
| Modules | 60 |
| Total unique questions | 1,470 |
| Reading & Writing | 810 |
| Mathematics | 660 |
| Presented per full attempt | 98 |
