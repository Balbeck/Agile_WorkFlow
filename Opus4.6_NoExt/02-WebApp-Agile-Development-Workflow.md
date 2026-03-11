# Web App Development Workflow — React + Node.js Through the Agile Method

## A Step-by-Step Evolutionary Guide

This document is both a technical development guide and an Agile learning journey. Each step builds on the previous one, delivering a working increment while teaching a core aspect of Agile product creation. By the end, you will have built a functional web application **and** internalized the Agile mindset.

---

## Overview of the Tech Stack

| Layer | Technology | Role |
|---|---|---|
| Frontend | React (Vite or Next.js) | User interface and interaction |
| Backend | Node.js + Express | API and business logic |
| Database | PostgreSQL or MongoDB | Data persistence |
| Auth | JWT + bcrypt | User authentication |
| Testing | Jest, React Testing Library, Supertest | Quality assurance |
| CI/CD | GitHub Actions | Automated build, test, deploy |
| Deployment | Vercel (frontend) + Railway/Render (backend) | Production hosting |

---

## Step 0 — Product Discovery (Sprint 0)

### Agile Concept: Vision, Personas, and Story Mapping

Before writing code, answer three questions: **Why** does this product exist? **Who** is it for? **What** problem does it solve?

### What You Do

- Write a **Product Vision Statement**: "For [target user] who [need], our product is a [category] that [key benefit]. Unlike [alternative], we [differentiator]."
- Create **2–3 User Personas** with names, goals, frustrations, and technical comfort levels.
- Run a **Story Mapping** session: lay out the user journey horizontally (steps the user takes) and vertically (depth of features for each step). The top row becomes your MVP.
- Produce a **Lean Canvas** (one-page business model).

### Output

A clear product vision, a set of personas, a user story map, and an initial Product Backlog with 15–30 user stories organized into epics.

### Key Takeaway

> You don't start Agile by building. You start by understanding.

---

## Step 1 — Project Scaffolding and Walking Skeleton (Sprint 1)

### Agile Concept: The Walking Skeleton and Definition of Done

A Walking Skeleton is the thinnest possible end-to-end implementation: a React page that calls a Node.js API that touches the database and returns something to the screen. It proves the architecture works before you invest in features.

### What You Build

```
project-root/
├── client/                  # React app (Vite)
│   ├── src/
│   │   ├── App.jsx
│   │   ├── components/
│   │   ├── pages/
│   │   ├── services/       # API call layer (axios/fetch)
│   │   └── main.jsx
│   └── package.json
├── server/                  # Node.js + Express
│   ├── src/
│   │   ├── index.js         # Express entry point
│   │   ├── routes/
│   │   ├── controllers/
│   │   ├── models/
│   │   └── middleware/
│   └── package.json
├── .github/workflows/       # CI/CD pipeline
├── .env.example
└── README.md
```

### Tasks

- Initialize React app with Vite: `npm create vite@latest client -- --template react`
- Initialize Express server: `npm init` + install express, cors, dotenv
- Create a single `/api/health` endpoint that returns `{ status: "ok" }`
- Create a React component that calls this endpoint and displays the result
- Set up ESLint and Prettier on both sides
- Write your first test (health endpoint returns 200)
- Define your **Definition of Done** as a team

### Definition of Done (Example)

- Code is written and passes linting
- Unit tests are written and passing
- Code is reviewed by at least one peer
- Feature is deployed to staging environment
- Product Owner has accepted the story

### Key Takeaway

> Sprint 1 is about proving the architecture, not building features. If the skeleton walks, everything else is incremental.

---

## Step 2 — User Authentication (Sprint 2)

### Agile Concept: User Stories, Acceptance Criteria, and Sprint Planning

This is where you practice writing proper user stories with clear acceptance criteria, estimating with story points, and running your first real Sprint Planning session.

### User Stories

**US-001:** As a new visitor, I want to create an account so that I can access personalized features.
- AC1: Registration form collects email, password, and display name
- AC2: Password is hashed before storage (bcrypt)
- AC3: Duplicate emails are rejected with a clear error message
- AC4: Successful registration redirects to login

**US-002:** As a registered user, I want to log in so that I can access my account.
- AC1: Login validates credentials and returns a JWT token
- AC2: Invalid credentials show an appropriate error
- AC3: JWT is stored securely (httpOnly cookie preferred)

**US-003:** As a logged-in user, I want to see a protected dashboard so that I know I'm authenticated.
- AC1: Unauthenticated requests to /dashboard redirect to /login
- AC2: Dashboard displays the user's display name

### What You Build

**Backend:** User model, registration route, login route, JWT middleware, protected route example.

**Frontend:** Registration page, Login page, Auth context (React Context or Zustand), Protected route wrapper, basic Dashboard shell.

### Key Takeaway

> Every feature starts as a user story. If you can't articulate who wants it and why, you probably shouldn't build it yet.

---

## Step 3 — Core Feature: Data Model and CRUD (Sprint 3–4)

### Agile Concept: Backlog Refinement and Prioritization (MoSCoW)

This is where the product starts to take shape. You build the core entity of your application — the thing users actually came for. The exact entity depends on your product (tasks, articles, projects, listings...), but the pattern is universal.

### Backlog Refinement Process

Before sprinting, the team refines upcoming stories:
- Break large stories into smaller ones (each completable in 1–3 days)
- Add detailed acceptance criteria
- Estimate using Planning Poker (Fibonacci: 1, 2, 3, 5, 8, 13)
- Prioritize using MoSCoW: Must Have, Should Have, Could Have, Won't Have (this time)

### What You Build

**Backend:**
- Data model with schema validation (Mongoose or Sequelize/Prisma)
- Full CRUD API: POST, GET (list + detail), PUT/PATCH, DELETE
- Input validation middleware (Joi or Zod)
- Error handling middleware with consistent error response format
- Pagination for list endpoints

**Frontend:**
- List view with data fetching (React Query or SWR recommended)
- Detail view
- Create/Edit form with client-side validation
- Delete confirmation flow
- Loading states, error states, empty states

### Key Takeaway

> Backlog refinement is where quality is born. Well-refined stories lead to predictable sprints. Poorly defined stories lead to chaos.

---

## Step 4 — UI/UX Polish and Design System (Sprint 5)

### Agile Concept: Sprint Review, Stakeholder Feedback, and Adaptation

After delivering raw functionality, this sprint focuses on usability. This is also where you practice the Sprint Review: demonstrating working software to stakeholders and using their feedback to adjust the backlog.

### What You Build

- Implement a design system or component library (Tailwind CSS, shadcn/ui, or custom)
- Responsive layout (mobile-first approach)
- Consistent typography, spacing, and color system
- Navigation: header, sidebar, or tab-based depending on product needs
- Toast notifications for user feedback (success, error, info)
- Accessibility basics: semantic HTML, ARIA labels, keyboard navigation, color contrast

### Sprint Review Checklist

- Demo the product to stakeholders (not a slideshow — live working software)
- Gather feedback: What works? What's confusing? What's missing?
- Document feedback as new stories or refinements to existing ones
- Re-prioritize the backlog based on what you learned

### Key Takeaway

> The Sprint Review is not a status meeting. It's a feedback machine. The quality of your next sprint depends on the honesty of this conversation.

---

## Step 5 — Testing Strategy and Quality (Sprint 6)

### Agile Concept: Technical Excellence and Sustainable Pace

Agile Principle #9 says continuous attention to technical excellence enhances agility. This sprint is dedicated to building a testing safety net that allows you to move fast without breaking things.

### The Testing Pyramid

```
         ╱  E2E Tests  ╲        ← Few, slow, high confidence
        ╱  (Cypress/Playwright) ╲
       ╱────────────────────────╲
      ╱   Integration Tests      ╲     ← Moderate count
     ╱   (Supertest + RTL)        ╲
    ╱──────────────────────────────╲
   ╱      Unit Tests                ╲   ← Many, fast, focused
  ╱      (Jest + RTL)                ╲
 ╱────────────────────────────────────╲
```

### What You Build

- **Unit tests** for utility functions, validation logic, and isolated components
- **Integration tests** for API endpoints (Supertest) and component interactions (React Testing Library)
- **End-to-end test** for the critical user path (registration → login → create item → view item)
- **CI pipeline** (GitHub Actions) that runs tests on every pull request
- Code coverage reporting (aim for 70–80% on critical paths, not 100% everywhere)

### Key Takeaway

> Tests are not overhead — they are the foundation of sustainable speed. A team without tests is a team that will slow down exponentially over time.

---

## Step 6 — Real-Time Features and Advanced Patterns (Sprint 7–8)

### Agile Concept: Spikes, Technical Stories, and Managing Uncertainty

When the team faces a technical unknown (Can we do real-time? How does WebSocket scale?), they run a **Spike** — a time-boxed research task. Spikes reduce risk before committing to full implementation.

### What You Build

- **WebSocket integration** (Socket.io) for real-time notifications or live updates
- **Role-based access control** (admin, editor, viewer)
- **File upload** (Multer + cloud storage like S3 or Cloudinary)
- **Search and filtering** (full-text search or Elasticsearch for scale)
- **Caching layer** (Redis for frequently accessed data)

### Spike Template

```markdown
## Spike: [Topic]
**Goal:** Answer the question: [specific question]
**Time-box:** [4 hours / 1 day / 2 days]
**Outcome:** A written summary with a recommendation and proof of concept (if applicable)
```

### Key Takeaway

> Not every task is a user story. Spikes, technical stories, and enablers are legitimate backlog items that keep the team from building on shaky ground.

---

## Step 7 — Performance, Monitoring, and Production Readiness (Sprint 9)

### Agile Concept: Definition of Done Evolution and Operability

As the product matures, the Definition of Done should evolve to include operational concerns: monitoring, logging, performance, and security.

### What You Build

- **Performance optimization:** Code splitting (React.lazy), image optimization, API response caching, database query optimization (indexes)
- **Error tracking:** Sentry or similar for both frontend and backend
- **Logging:** Structured logging (Winston or Pino) with log levels
- **Health checks and uptime monitoring**
- **Security hardening:** Helmet.js, rate limiting, CORS configuration, input sanitization, dependency audit (npm audit)
- **Environment management:** Separate configs for development, staging, and production

### Evolved Definition of Done

- All previous DoD items, plus:
- Feature is monitored (errors are captured)
- Performance is acceptable (page load < 3s, API response < 500ms)
- Security checklist is reviewed
- Runbook is updated if operational procedures changed

### Key Takeaway

> A feature that works on your laptop but crashes in production is not done. Operability is a feature.

---

## Step 8 — Release, Launch, and Continuous Improvement (Sprint 10+)

### Agile Concept: Continuous Delivery, Retrospectives, and the Infinite Game

The product is never "finished." Agile treats delivery as a continuous flow, not a one-time event. The launch is a milestone, not an endpoint.

### What You Do

- **Deploy to production** with a CI/CD pipeline (automated tests → staging → production)
- **Feature flags** for gradual rollout (LaunchDarkly, Unleash, or simple env-based flags)
- **Analytics** to measure real usage (Mixpanel, PostHog, or simple event tracking)
- **User feedback loop:** In-app feedback widget, user interviews, NPS surveys
- **Retrospective:** What did we learn from the entire journey? What would we do differently?

### Retrospective Format (Start/Stop/Continue)

| Start Doing | Stop Doing | Continue Doing |
|---|---|---|
| More pair programming | Skipping code review under pressure | Daily standups |
| User testing every sprint | Overcommitting in sprint planning | Writing tests before merging |
| Documenting architectural decisions | Working on weekends | Weekly backlog refinement |

### Key Takeaway

> The best Agile teams are not the ones that ship the most features. They are the ones that learn the fastest.

---

## Future Features Roadmap — What Comes Next

Once the core product is stable and users are engaged, here are high-value features to consider for future sprints. These are intentionally left as epics to be refined when the time comes.

### Short Term (Next 2–3 Sprints)

- **Collaborative features:** Multi-user editing, commenting, @mentions
- **Notification system:** Email + in-app notifications for key events
- **Dashboard and analytics:** User-facing metrics and activity summaries
- **Dark mode and theming:** User preference for visual customization

### Medium Term (Next Quarter)

- **API for third-party integrations:** RESTful or GraphQL API with API key management
- **Mobile responsiveness improvements** or dedicated React Native app
- **Internationalization (i18n):** Multi-language support
- **Advanced search** with filters, sorting, and saved searches
- **Onboarding flow:** Guided tour for new users

### Long Term (Future Vision)

- **AI-powered features:** Smart suggestions, content generation, predictive analytics
- **Marketplace or plugin system:** Allow third parties to extend the product
- **Offline support:** Service workers and local-first architecture
- **Enterprise features:** SSO (SAML/OIDC), audit logs, team management, advanced permissions

---

## Summary — The Development Journey at a Glance

| Step | Sprint | Agile Concept | Technical Deliverable |
|---|---|---|---|
| 0 | Sprint 0 | Product Discovery | Vision, Personas, Story Map, Backlog |
| 1 | Sprint 1 | Walking Skeleton, DoD | Project scaffolding, end-to-end connection |
| 2 | Sprint 2 | User Stories, Sprint Planning | Authentication system |
| 3 | Sprint 3–4 | Backlog Refinement, MoSCoW | Core CRUD features |
| 4 | Sprint 5 | Sprint Review, Feedback Loop | UI/UX polish, design system |
| 5 | Sprint 6 | Technical Excellence | Testing strategy and CI pipeline |
| 6 | Sprint 7–8 | Spikes, Technical Stories | Real-time features, advanced patterns |
| 7 | Sprint 9 | DoD Evolution | Performance, monitoring, security |
| 8 | Sprint 10+ | Continuous Delivery | Launch, analytics, continuous improvement |

---

*This document is part of the Agile Workflow Project — a step-by-step guide to product creation through the Agile method.*
