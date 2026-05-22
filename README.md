# Hi, I'm Annika Holmqvist

**Backend Developer** building secure, scalable software with Java, Spring, and cloud-native architecture. Currently finishing my backend developer education while running two businesses on the side - so I care a lot about shipping things that actually work in production.

Gothenburg, Sweden · Open to backend and full-stack opportunities

---

## What I'm working on

- **Eloize Audit Platform** - Production system for Eloize AB that powers the AI Growth Audit product.
- **Devroom** - A distributed chat application where users @mention AI mentors that respond to questions. Five Spring Boot services plus a Next.js frontend, secured with OAuth2 end-to-end and deployable to
  Kubernetes with a single command.
- **Nordic Dev Mentor** - A Spring Boot middleware proxying OpenRouter chat with four AI mentor personalities, paired with a Next.js frontend (Spring Boot 4, Java 21, Next.js 16, React 19, Tailwind 4, Railway)
- **Vet1177** - A veterinary case management system with ABAC security (Java 24, Spring Boot 4, PostgreSQL, MinIO)
- Collaborating with teams using feature-branch workflows, PR reviews, and CI/CD pipelines

---

## Core Stack

**Backend:** Java · Spring · Spring Security · JPA/Hibernate · JWT (ES256) · OAuth2 Resource Server · REST APIs<br>
**AI & Integrations:** Anthropic Claude API · Perplexity API · MCP servers · OkHttp · Spring WebFlux WebClient · PDFBox · Apache POI<br>
**Automation:** n8n · Make.com · GitHub Actions<br>
**Databases:** PostgreSQL (incl. JSONB) · Supabase · Azure SQL · MySQL · HikariCP<br>
**Storage & Files:** Supabase Storage · MinIO (S3-compatible) · AWS SDK v2<br>
**Frontend:** React · TypeScript · Vite · Tailwind CSS · Recharts<br>
**DevOps:** Docker · Docker Compose · Railway · Vercel · Azure App Service · Kubernetes · Testcontainers<br>
**Practices:** REST API design · Async orchestration · ABAC authorization · TDD · SOLID · Clean architecture

---

## Featured Projects

### Eloize Audit Platform - AI-Powered Growth Audits

Production system for Eloize AB that powers the AI Growth Audit product. A Spring Boot backend orchestrates Claude to generate multi-section audit reports from uploaded documents and client interviews, with two separate React frontends - one internal tool for consultants, one client-facing portal. Deployed and running in production on Railway + Vercel.

> *This is a commercial project - all repositories are private. Architecture and technical details are documented below. Happy to walk through the code and demo the live system in an interview.*

**Backend:** Java 21 · Spring Boot 4 · Spring Data JPA · Supabase PostgreSQL · Anthropic Claude API · OkHttp · WebFlux WebClient · Jackson (JSONB mapping) · Railway<br>
**Frontends:** React · TypeScript · Tailwind CSS · Recharts · Axios · Vercel<br>
**Storage:** Supabase Storage for PDF/DOCX/TXT uploads (up to 25 MB) · PDFBox & Apache POI for server-side text extraction<br>

**Architecture highlights:**
- **Async AI orchestration** - Dedicated `newFixedThreadPool(3)` for Claude API calls to avoid starving Tomcat threads. Generates six report sections sequentially with dependency passing (e.g. `WORKFLOW_INVENTORY` numbers feed into `EXECUTIVE_SUMMARY`)
- **Graceful degradation** - Section failures are logged and the pipeline continues rather than failing the whole audit
- **Single-source-of-truth dashboard** - `DashboardService` aggregates AI outputs into one endpoint so the UI doesn't recompute across sections
- **Auto-generated workflows on publish** - Publishing an audit synchronously triggers generation of 3–5 automation workflows, including n8n-compatible JSON templates
- **JSONB domain mapping** - Client profiles and audit metadata stored as PostgreSQL JSONB, mapped via Jackson with `@JdbcTypeCode(SqlTypes.JSON)`
- **Public + authenticated endpoints** - Clients access published audits via short access codes (`ABC-1234`); pre-interview forms use one-time tokens
- **Manual schema management** with `ddl-auto=validate` and explicit cascade delete logic in `AuditService` to match business semantics
- **Slack bot integration** - Protected API endpoints allow an internal AI agent to manage audits directly from Slack
  
**Three deployment units:**
- **Backend** (Java/Spring Boot) - REST API, AI orchestration, data layer → Railway
- **Internal Portal** (React) - consultant dashboard with file uploads, AI section review, and publication workflow → Vercel
- **Client Portal** (React) - client-facing app with access-code sign-in and Recharts visualizations → Vercel

**API surface:** 40+ REST endpoints across `/api/clients`, `/api/audits`, `/api/audits/{id}/workflows`, `/api/files`, `/api/forms`, and `/api/public/*` - full API documentation available on request.

---

### [Devroom](https://github.com/annikaholmqvist94/devroom)

  A distributed chat application where users @mention AI mentors that respond to questions. Five Spring Boot services plus a Next.js frontend, secured with OAuth2 end-to-end and deployable to
  Kubernetes with a single command. Integrates my earlier Nordic Dev Mentor service as a black-box LLM dependency.

  Stack: Spring Boot 4 · Java 21 · Spring Authorization Server · Spring Cloud Gateway · Spring gRPC · RabbitMQ · PostgreSQL 16 · Next.js 16 · React 19 · Tailwind 4 · TypeScript · Kubernetes
  (Minikube) · Docker

  Highlights

  - OAuth2 end-to-end - Spring Authorization Server issues RS256 JWTs, Resource Servers validate via JWKS, Gateway runs Authorization Code + PKCE with cookie-based BFF sessions so the browser
  never sees a token
  - Transactional outbox for signup - atomic DB write plus at-least-once publish to RabbitMQ plus idempotent consumer in User Service guarantees no ghost users on partial failures
  - Bounded contexts with a separate Postgres instance per service (auth-db, user-db, message-db) and no foreign keys across DB boundaries
  - gRPC for internal read traffic (Message and Bot Service look up users via Spring gRPC 1.0.3), REST for writes
  - Bot Service uses OAuth2 Client Credentials with `bot:write` scope - consumes `message.published` events from RabbitMQ, looks up sender via gRPC, calls Nordic Dev Mentor, posts replies back
  through Message Service
  - Multi-stage Docker builds with BuildKit cache mounts, plus 14 Kubernetes manifests (StatefulSets for Postgres, Deployments for stateless services, Secrets rendered from templates)
  - One-command deploy - `bash k8s/deploy.sh` takes a fresh Minikube to a running 11-pod cluster in ~5 minutes
  - 9 ADRs documenting every architectural choice with alternatives considered (OAuth2 stack chosen over Kong and handwritten JWT after weighing 8 options, gRPC vs REST per traffic category,
  Gateway WebMVC vs WebFlux)
  - Testcontainers-based integration tests per service - real Postgres and RabbitMQ in CI, not mocks

---

 ### [Nordic Dev Mentor](https://github.com/annikaholmqvist94/nordic-dev-mentor)

  A Spring Boot middleware that proxies chat requests to OpenRouter with four distinct AI mentor personalities, paired with a Next.js frontend in editorial Nordic
   design. Deployed as two Railway services with the backend reachable only via internal DNS - the API key never leaves the server.                               
                  
  Stack: Spring Boot 4 · Java 21 · Spring RestClient · Spring Data Redis · Next.js 16 · React 19 · Tailwind 4 · TypeScript · Spring Data Redis                  
  
  Highlights                                                                                                                                                      
                  
  - Hexagonal architecture - domain layer has no Spring imports                                                                                                   
  - Per-personality system prompts and sampling temperature
  - PII filter masks email, Swedish personnummer (Luhn-validated), and Swedish phone numbers before input is forwarded to the LLM
  - Pluggable conversation store with sliding-window history - in-memory by default, Redis opt-in via env var                                                     
  - Exponential-backoff retry with Idempotency-Key for OpenRouter resilience                                                                                      
  - localStorage-backed conversation history with click-to-resume                                                                                                 
  - 55 backend tests (JUnit 5 + WireMock + MockMvc + Mockito) with JaCoCo coverage, 26 frontend tests (Vitest + RTL)

  [Live demo](https://frontend-production-25e3.up.railway.app/) 

---

### [Vet1177 — Veterinary Case Management System](https://github.com/ithsjava25/project-backend-org-random-coders)

A full-stack web application for managing veterinary case records. Pet owners create and track medical cases for their animals, veterinarians manage and respond to cases at their clinic, and admins have full system oversight. Built as a group project with file attachments, real-time activity log, role-based access control, and a full REST API — all containerized and ready to run with a single command.

**Backend:** Java 24 · Spring Boot 4.0.4 · Spring Security · OAuth2 Resource Server · PostgreSQL 15 · MinIO (S3-compatible) · AWS SDK v2 · Docker Compose · GitHub Actions CI/CD
**Frontend:** React 19 · Vite 8 · Tailwind CSS · Axios · jwt-decode
**Highlights:**
- Policy-based ABAC authorization layer with per-entity policies
- Custom exceptions mapped to HTTP semantics (400/401/403/404/422) via `@RestControllerAdvice`
- Activity log / audit trail on all case events
- 150+ feature branches, 115+ PRs merged across a 4-person team
- Documented `API.md` and environment-driven configuration

Built with [@lindaeskilsson](https://github.com/lindaeskilsson), [@TatjanaTrajkovic](https://github.com/TatjanaTrajkovic), and [@johanbriger](https://github.com/johanbriger).

---

### TalentFlow Pro — Full-Stack ATS Application

A cloud-native Applicant Tracking System demonstrating the full lifecycle of modern software development — from secure backend logic to automated deployment and real-time candidate management.

**Stack:** Java · Spring Boot · Supabase (PostgreSQL + JWT ES256) · React · TypeScript · Tailwind CSS · Railway · Vercel
**Highlights:**
- Token-based security with Supabase JWT authentication (ES256)
- Row Level Security on the database layer
- Drag-and-drop recruitment pipeline with stage management
- Detailed candidate scorecards and role-based admin controls
- Fully automated deployment via Railway CLI and Vercel

 [Backend repo (mini-ATS)](https://github.com/annikaholmqvist94/mini-ATS) · [Frontend repo (talentflow-pro)](https://github.com/annikaholmqvist94/talentflow-pro)

---

### [MeetingApp — Meeting Management Platform](https://github.com/annikaholmqvist94/meetingapp)

A full-stack meeting management application with a dark glassmorphism UI, Kanban board with drag-and-drop, dashboard with statistics, and calendar view.

**Stack:** Java 21 · Spring Boot · Spring Data JPA · Thymeleaf · PostgreSQL · Docker

---

### [Invoice Management System (Team Project)](https://github.com/ithsjava25/project-jpa-grupp-3-d)

A comprehensive invoice management solution built with clean architecture principles and modern Java practices. Collaborative project focused on JPA relationships and system design.

Built with [@kristina0x7](https://github.com/kristina0x7) and [@fmazmz](https://github.com/fmazmz).

---

### [Warehouse & CLI Apps](https://github.com/annikaholmqvist94/CLI-app)

Core Java fundamentals in focus — Object-Oriented Design, efficient data handling, and Test Driven Development with JUnit.

**Stack:** Java · JUnit · JDBC · Testcontainers · Docker

---

---

## Connect with Me

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Annika%20Holmqvist-blue?style=for-the-badge&logo=linkedin)](https://www.linkedin.com/in/annika-holmqvist-130911209/)
[![Email](https://img.shields.io/badge/Email-annika.holmqvist94@gmail.com-red?style=for-the-badge&logo=gmail)](mailto:annika.holmqvist94@gmail.com)

---
