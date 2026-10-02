# AnnaSetu: Engineering Journey Roadmap

> Mentor-designed plan, created Fri 2 Oct 2026. Covers about 17 weeks, to the end of January 2027.
> Learning loop for every topic: **BUILD → UNDERSTAND → BREAK → FIX → DOCUMENT**
> Rule: no technology goes in unless it solves a problem we can see in the current version.

---

## 0. Reality check (read this first)

| Fact | Consequence |
|---|---|
| Today is **2 Oct**. Companies may start visiting in **Oct/Nov**. | The "interview-ready" window is about **6 weeks** away, not 4 months. Phase 1–2 are tight and focused. |
| The repo (`RePlate`) is **empty**. | V1 starts from zero. Good: every decision in it will be yours and explainable. |
| You have **~16.5 h/week backend+project** and **~10 h/week AI**. | Two parallel tracks. They meet at V8, when the backend calls the ML service. |
| Most backend slots are **11 PM – 2 AM**. | New, hard concepts go in **daytime/evening** slots. Late-night slots are for verification, recall and debugging drills. |
| Claude Code writes the code. | Your job is to **inspect, test, break, explain**. Every Claude Code run ends with you reading the diff. |
| No real donation data exists. | ML uses a **synthetic data generator** with realistic patterns. Be honest about this in interviews; it's a strength if you can say how you'd collect real data. |

---

## 1. Timetable analysis

### Hours per track (approx.)
| Track | Slots | Hours/week |
|---|---|---|
| Backend | Mon 11:30p–2a (2.5), Tue 1–2a (1), Thu 1–2a (1), Fri 5:30–7p (1.5), Sat (2), Sun (2.5) | ~10.5 |
| Project | Sat (2.5), Sun (3.5) | ~6 |
| AI | Mon 9–11:30p (2.5), Tue 5–7p (2), Wed 1–2:30a (1.5), Thu 9–11p (2), Fri 9–11p (2) | ~10 |
| DSA / Core | as per your sticky notes; this roadmap doesn't touch them | — |

### Issues I see
1. **Monday overlap.** AI runs until 11:30 PM, but backend starts at 11:00 PM. Treat backend as **11:30 PM–2:00 AM**.
2. **Monday is the heaviest night**: class 5:30–8:30, AI 2.5 h, then backend 2.5 h. Monday backend does the *implementation* of a concept you already learned on Fri/Sat. It doesn't introduce new theory.
3. **1–2 AM slots** (Tue backend, Wed AI, Thu backend) are low-energy. Use them for recall quizzes, reading code Claude wrote, small fixes, and writing ADRs, never for brand-new concepts.
4. **Sleep.** You're ending at 2–2:30 AM nearly every night. If a week collapses, cut the late-night slot first, not the weekend project slot.

### How a backend week runs (a "week" starts on Friday)
| Slot | Energy | Loop stage | What happens |
|---|---|---|---|
| **Fri 5:30–7:00 PM** | fresh | UNDERSTAND | New concept of the week, plus diagnostic questions |
| **Sat Backend 2h + Project 2.5h** | fresh | BUILD | Claude Code implements, you inspect the diff and test manually |
| **Sun Project 3.5h** | fresh | BREAK → FIX | Deliberate failure, debugging, then the fix |
| **Sun Backend 2.5h** | medium | DOCUMENT + INTERVIEW | ADR, notes, Interview Mode, PROGRESS.md update |
| **Mon 11:30 PM–2 AM** | tired | BUILD (extension) | Second, smaller piece of the week's feature |
| **Tue 1–2 AM** | low | RECALL | 5 reasoning questions plus a small fix |
| **Thu 1–2 AM** | low | DEBUG DRILL | I give you a bug or scenario, you reason it out |

### How an AI week runs
| Slot | Use |
|---|---|
| **Tue 5–7 PM** (freshest) | Hardest new concept of the week |
| **Mon 9–11:30 PM** | Notebook practice on that concept |
| **Thu 9–11 PM** | Implementation (script/model/API) |
| **Fri 9–11 PM** | Mini-deliverable + quiz |
| **Wed 1–2:30 AM** | Recall, re-run notebooks, read docs |

**Buffer rule:** about every 4th week is lighter (consolidation, catch-up). Tell me exam dates and I'll move the buffers onto them.

---

## 2. Likely prerequisite gaps (to be confirmed on Day 1)

Based on "React/JS known, some Node/Express exposure, tutorial-heavy, low implementation":

| Area | Likely gap | Why it matters |
|---|---|---|
| HTTP | Status codes, headers, idempotent methods, statelessness | Every API design and interview question sits on this |
| Async JS | Event loop, promise rejection, errors in async handlers | The #1 cause of "my Express server crashed" |
| Express internals | Middleware chain, `next()`, error middleware signature | Auth, validation and logging are all middleware |
| Data modeling | Embed vs reference, schema design for state changes | Donation lifecycle is a state machine |
| Indexes | What an index *is* (B-tree), why queries get slow | Prerequisite for caching. **No Redis before this.** |
| Concurrency | Two requests touching the same document | "Two NGOs claim same donation" is the best interview story in this project |
| Git | Branches, meaningful commits, PR flow | Your GitHub is part of your interview |
| Python/pandas | Probably light | Needed before any ML |
| Stats for ML | Mean/variance/distributions, why we split data | Needed to *evaluate* a model, not just train it |
| Networking | Ports, DNS, TLS, env vars | Needed for deployment |

---

## 3. The 4-month roadmap

### PHASE 1: Backend Foundation → V1 + V2 (Weeks 1–3 · 2 Oct – 22 Oct)

**AnnaSetu:** V1 donation listing (provider creates/edits/closes; NGO browses) → V2 accounts & roles.

| Week | Backend track | AI track |
|---|---|---|
| W1 | HTTP + request lifecycle, Express layered architecture (routes → controllers → services → models), centralized error handling, MongoDB + Mongoose, Donation model, CRUD | Python refresher (fast), NumPy essentials, pandas basics on a synthetic donations CSV |
| W2 | Validation (zod), donation **status state machine** (AVAILABLE → CLAIMED → PICKED_UP / EXPIRED / CANCELLED), pagination + filtering, **Jest + Supertest** basics, **atomic claim** (`findOneAndUpdate` with a status condition) | pandas: groupby, time features, cleaning, plotting. Build the **synthetic data generator** for restaurant surplus |
| W3 | V2: authN vs authZ, bcrypt, JWT access + refresh, auth middleware, **RBAC** (provider/NGO/volunteer/admin), **ownership checks**, basic security (helmet, CORS, input limits). **Quick deploy** (Render/Railway + MongoDB Atlas): live URL | ML foundations: what learning is, regression vs classification, features/labels, **train/test split**, baseline model, leakage |

**Pulled forward on purpose:** the *claim race condition* (from V13) and *testing* go into Phase 1. Both are cheap now, both are top interview material, and tests are what make BREAK → FIX measurable.

**You should be able to explain:** the request lifecycle; why controllers and services are separate; why a 4-argument error middleware; JWT flow and where tokens live; RBAC vs ownership; how an atomic update prevents a double claim.

---

### PHASE 2: Product Logic + Production Basics → V3 + V4 + V5 (Weeks 4–6 · 23 Oct – 12 Nov)

| Week | Backend track | AI track |
|---|---|---|
| W4 | V3 deterministic **matching**: filter eligible NGOs, a weighted scoring function, ranking. **Indexes**: seed 50k docs, use `explain()`, compound indexes, ESR rule | Model evaluation: MAE/RMSE, precision/recall/F1, confusion matrix, **overfitting/underfitting**, cross-validation |
| W5 | V4 **geo**: GeoJSON, `2dsphere`, `$geoNear`, distance in scoring, map on frontend (Leaflet + OSM, free) | **V8 offline:** surplus prediction model (sklearn pipeline, compare vs naive baseline), `joblib` serialization |
| W6 | V5: **Docker** (Dockerfile, compose with Mongo), env vars/secrets, **GitHub Actions CI** (lint + tests), structured logging (pino), `/health`, HTTPS (handled by platform), deploy | **FastAPI** inference service for the surplus model. Input validation (pydantic). Dockerize it |

**🎯 OCT/NOV READINESS CHECKPOINT (end of W6, ~12 Nov).** See section 4.

---

### PHASE 3: Performance + Async + LLM Basics → V6 + V7 (Weeks 7–9 · 13 Nov – 3 Dec)

| Week | Backend track | AI track |
|---|---|---|
| W7 | V6: **load test** (autocannon/k6) the hot endpoint (NGO feed / matching). Find the bottleneck, *then* **Redis cache-aside**, TTL, invalidation on donation change, measure before/after. Kill Redis → graceful fallback | **LLM fundamentals:** tokens, context window, temperature, cost/latency, prompting, **structured output** |
| W8 | **Rate limiting** (Redis-backed, login + claim endpoints). V7: notifications made slow on purpose → API slow → **queue + worker** (BullMQ, because Redis already exists; *not* Kafka) | Real feature: **free-text donation → structured fields** ("40 plates veg biryani cooked 2h ago") via LLM with schema validation + **fallback to manual form** |
| W9 *(lighter)* | V7 deeper: retries + backoff, **dead-letter queue**, **idempotency** (duplicate job processing), Node ↔ FastAPI call with **timeout + fallback** | **Tool calling**; embeddings concept; consolidation + revision |

---

### PHASE 4: ML in the Product → V8 integration + V9 + V10 (Weeks 10–13 · 4 Dec – 31 Dec)

| Week | Focus |
|---|---|
| W10 | V8 integrated: provider dashboard shows predicted surplus. Async vs sync decision (precompute nightly vs on-demand) |
| W11 | V9 urgency: **first build a rule-based version**, then ask whether ML beats it. Classification, class imbalance, cost of false negatives (unsafe food marked "not urgent") |
| W12 | V10 intelligent matching: offline evaluation of ranking quality (precision@k, acceptance rate). Add a "probability NGO accepts" model as *one feature* in the deterministic score |
| W13 *(lighter)* | Embeddings + **RAG** (small, isolated feature with guardrails), MLflow experiment tracking + model versions (local), **drift** concept with a simple check |

---

### PHASE 5: Failure, Architecture, System Design → V13 + V11 + V14 (Weeks 14–17 · 1 Jan – end Jan)

| Week | Focus |
|---|---|
| W14 | V13 failure engineering: chaos drills (kill Redis, worker, ML service, DB). Timeouts, retries with jitter, circuit breaker concept, consistency |
| W15 | V11 microservices: split **only** what earned it (ML service is already separate; notification worker). Gateway via nginx, service-to-service auth, DB ownership. **Kafka: design-level + small demo**, compared against BullMQ |
| W16 | V14 system design: 20 cities, 2M users. Requirements, back-of-envelope estimates, sharding/partitioning by city, read replicas, CDN, observability |
| W17 | Polish: README, architecture diagram, ADRs, demo video, **mock interviews** on all 10 final questions |

---

## 4. Targets

### 🎯 OCT/NOV READINESS TARGET (~12 Nov)
You can:
- Give a 2-minute **AnnaSetu pitch** with a **live deployed link** and a clean GitHub repo (tests, CI badge, README, ADRs)
- Walk through any request end to end: client → middleware → controller → service → DB → response/error
- Explain JWT auth, refresh tokens, bcrypt, RBAC vs ownership, and common attacks
- Explain the **double-claim race condition** and your atomic fix
- Explain your **matching score** and why it's deterministic (not ML)
- Explain an **index** you added, with `explain()` numbers before and after
- Explain Docker, env/secrets, and what your CI does
- ML: explain the surplus model end to end: data → features → split → baseline → model → metric → serialization → FastAPI
- Answer: "Why not ML for matching?" "Why not Redis yet?" "Why not microservices?" (knowing when *not* to is a senior signal)

**Stretch by end of Nov:** Redis caching + queue (V6/V7) and the LLM structured-extraction feature.

### 🎯 DEC/JAN DEEPENING TARGET
- ML genuinely integrated into product decisions, with fallbacks and evaluation
- Failure engineering drills documented with results
- Justified service split and a Kafka vs BullMQ trade-off you can argue
- Full V14 system design doc you can whiteboard in 45 minutes
- Confident answers to all 10 final-challenge questions

---

## 5. Topic triage (your original list)

| Category | Topics |
|---|---|
| **ESSENTIAL** (before Nov) | HTTP, REST/API design, Express middleware, layered architecture, validation, error handling, MongoDB modeling, **indexes**, auth/JWT/bcrypt/RBAC, atomic operations, pagination, testing basics, Git/GitHub, Docker basics, deployment, env/secrets, logging basics, CI basics · pandas, sklearn, train/test, metrics, overfitting, FastAPI inference |
| **USEFUL** (Nov–Dec) | Redis caching, TTL, invalidation, rate limiting, queues/workers, retries, idempotency, geospatial, LLM structured output, tool calling, embeddings, RAG, WebSockets (only if real-time claim updates become a real need) |
| **OPTIONAL / ADVANCED** (Dec–Jan) | Kafka hands-on, microservices split, API gateway, MLflow, drift monitoring, Prometheus/Grafana, OpenTelemetry, learning-to-rank, vector DB as separate infra |
| **NOT NOW / UNNECESSARY** | Kubernetes, training deep nets from scratch, fine-tuning LLMs, GraphQL, multi-cloud, heavy math/statistics beyond what evaluation needs, TypeScript migration (useful later, adds friction now), complex frontend state libraries |

---

## 6. External material policy

- **Default: A or D.** Mentor explanation + implementation. No videos.
- **B (docs)** where docs beat everything: Express error-handling guide, MongoDB indexes/geospatial docs, FastAPI tutorial, scikit-learn user guide, Docker get-started.
- **C (video)** only where visuals add real value: likely **StatQuest** (bias/variance, cross-validation, metrics) and **Karpathy's "Intro to Large Language Models"** talk. The exact video and the sections to watch or skip get named when the topic arrives.

---

## 7. Persistence (important: Claude sessions start cold)

Each Claude session is fresh, so the repo is our memory:
- `docs/journey/ROADMAP.md`: this file
- `docs/journey/PROGRESS.md`: completed days, quiz results, **weak areas**, next day (created Day 1)
- `docs/decisions/NNN-*.md`: Architecture Decision Records (problem → options → choice → trade-offs)
- `CLAUDE.md`: rules for Claude Code in this repo (explain changes, no black boxes, small diffs)

Start every session with: *"Read docs/journey/PROGRESS.md and continue the journey."*

---

## 8. Day 1 plan (not taught yet, waiting for approval)

**Slot:** Fri 5:30–7:00 PM (1.5 h) · or Sat backend slot if today's is gone

| Time | Block |
|---|---|
| 20 min | **Diagnostic:** about 8 reasoning questions (HTTP, async JS, Express, MongoDB, auth). Calibrates the pace; no teaching yet |
| 25 min | **Concept:** what happens when an NGO's app calls `GET /api/donations`: HTTP anatomy, methods, status codes, statelessness, then the Express lifecycle: middleware → router → controller → service → model → response, plus the error path |
| 30 min | **Implementation (Claude Code):** backend skeleton. `app.js`/`server.js` split (and why), `/health`, request-logging middleware, 404 handler, central error handler, `.env.example`, `CLAUDE.md`, `PROGRESS.md`. First real commit |
| 10 min | **Break it:** give the error handler 3 params instead of 4, throw in a route, observe, explain, fix. Then send malformed JSON and look at what comes back |
| 5 min | Interview Mode (1 question) + Quick Recall (3 questions) → **STOP: DAY 1 COMPLETE** |

External material: **D, none.**
