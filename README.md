# CareerOS

**Your career. One intelligent workspace.**

CareerOS is a full-stack, AI-powered career and job-search workspace — designed, built and
deployed as a production-style portfolio project. It combines a resume builder, ATS analysis,
job matching, an AI interview studio, and a full application pipeline into one connected product.

**Live demo:** https://resume-hub-436.preview.emergentagent.com
Click **"Try Interactive Demo"** — no account needed. (Demo profile: Alex Morgan, Software Engineer.)

---

## Feature set

| Module | What it does |
|---|---|
| Resume Builder | Multi-resume editor with live preview, 5 ATS-friendly templates, reorder/duplicate, one-click PDF export |
| Resume Import | Upload a PDF or DOCX — GPT-5.4 parses it into fully editable structured data |
| Job Matcher | Paste any job description → match score, matched/missing skills, gap-closing suggestions |
| ATS Analysis | 6-dimension scoring with counted, evidence-quoting feedback ("2 bullets missing measurable achievements") |
| Resume Tailoring | Bullet-by-bullet rewrites targeting a specific JD — original vs. improved vs. why, apply in one click |
| Application Tracker | 6-stage Kanban (Saved → Offer/Rejected) with drag & drop, search, sort, notes |
| Company Tracker | Dossiers per target company: contacts, salary, notes, status |
| Interview Prep | AI interviewer persona scores every answer (clarity / depth / structure / impact), reacts live, and produces a report + personalized practice plan. Mock mode: 10 timed questions |
| Career Dashboard | Readiness score (87/100) with breakdown report, momentum charts, reminders, recommended actions |
| AI Career Coach | GPT-5.4 coach with workspace context, streaming SSE replies, persistent history |
| Skills & Roadmap | Animated skills matrix + guided milestone timeline |
| Projects / Portfolio | Project cards with AI-generated descriptions (Resume / LinkedIn / GitHub versions) |
| Analytics | Application funnel, match scores, readiness radar (Recharts) |
| Extras | Follow-up reminders, notifications, activity timeline, dark/light themes, visitor analytics, fully responsive |

## Tech stack

- **Frontend:** React 19, TypeScript (strict), Vite, Tailwind CSS v4, shadcn/ui, Framer Motion (motion), Lenis smooth scroll, Recharts, TanStack Query
- **Backend:** FastAPI (async), MongoDB (Motor), JWT auth in httpOnly cookies, bcrypt, brute-force lockout
- **AI:** GPT-5.4 via the Emergent universal key — SSE streaming chat, structured JSON extraction (resume parsing, ATS reports, answer evaluation) with offline heuristic fallbacks
- **Infra touches:** Kubernetes ingress routing, social OG/Twitter preview cards, privacy-friendly visitor analytics

## Architecture notes

- `frontend/src/services/ai.ts` — single AI boundary: every feature calls the backend first and
  falls back to deterministic local heuristics, so the demo never breaks
- `backend/routers/ai.py` — all LLM endpoints (chat SSE, parse-resume, evaluate-answer,
  analyze-resume, match, tailor, project-description)
- `frontend/src/context/CareerContext.tsx` — workspace state, persisted to localStorage, seeded
  with realistic demo data
- Auth: access (60 min) + refresh (7 d) httpOnly cookies; demo mode is a client-side session
  requiring no account

## Running locally

```bash
# backend
cd backend && uvicorn server:app --host 0.0.0.0 --port 8001 --reload
# frontend
cd frontend && yarn && yarn dev
```

Backend needs `MONGO_URL`, `DB_NAME`, `JWT_SECRET`, and `EMERGENT_LLM_KEY` in `backend/.env`.

---

*Designed & built end-to-end as a full-stack portfolio project — React · FastAPI · MongoDB · GPT-5.4.*
