# CleverHub SAT

Independent Digital SAT practice platform. Full-length adaptive mock examinations with realistic timing, module structure, and tools.

**Not affiliated with or endorsed by the College Board.**

## Stack

- **Frontend:** React, TypeScript, Vite, Tailwind CSS, Lucide, KaTeX
- **Backend:** Node.js, Express, TypeScript
- **Database:** PostgreSQL + Prisma
- **Deploy:** Render (Web Service + PostgreSQL)

## Local development

### Prerequisites

- Node.js 20+
- PostgreSQL 15+

### Setup

```bash
cp .env.example .env
# Edit DATABASE_URL, JWT_SECRET, etc.

npm install
npx prisma generate
npx prisma migrate dev --name init
# Optional: npm run db:seed  (when seed is available)

npm run dev
```

- API: http://localhost:3000  
- Client (Vite): http://localhost:5173 (proxies `/api` to the server)

### Production build

```bash
npm run build
NODE_ENV=production npm start
```

Server binds to `0.0.0.0` and uses `process.env.PORT`.

## Environment variables

See `.env.example`. Required in production:

- `DATABASE_URL`
- `JWT_SECRET`
- `NODE_ENV=production`
- `PORT` (set by Render)

Optional:

- `DESMOS_API_KEY` — authorised Desmos integration
- `RW_MODULE2_HIGH_THRESHOLD` / `MATH_MODULE2_HIGH_THRESHOLD` — adaptive routing (default 0.60)

## Render deployment

1. Push this repository to GitHub.
2. Create a Render Web Service from the repo (or use `render.yaml`).
3. Create a Render PostgreSQL database and link `DATABASE_URL`.
4. Set `JWT_SECRET` (and optionally `CLIENT_URL` if needed).
5. Build: `npm install && npx prisma generate && npm run build`
6. Start: `npx prisma migrate deploy && node server/dist/index.js`
7. Health check: `/api/health`

After first deploy, create an administrator securely (script or one-time seeded admin — do not hardcode passwords).

## Examination structure (per mock)

| Section | Module | Questions | Time |
|---------|--------|-----------|------|
| Reading & Writing | Module 1 | 27 | 32 min |
| Reading & Writing | Module 2 (adaptive) | 27 | 32 min |
| Break | — | — | 10 min |
| Mathematics | Module 1 | 22 | 35 min |
| Mathematics | Module 2 (adaptive) | 22 | 35 min |

Total presented: **98 questions**. Testing time: **134 minutes**.

Each mock stores **147 unique questions** (Module 1 + lower and higher Module 2 branches for both sections). Questions are never reused across mocks or branches.

## Project status

See [PROJECT_STATUS.md](./PROJECT_STATUS.md).

## Licence & disclaimer

Practice scores are **estimates** only. Adaptive thresholds and scoring conversions are documented approximations and are not official College Board formulas. All questions are original content created for this platform.
