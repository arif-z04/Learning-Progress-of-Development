# 11-Week Full-Stack Engineer To-Do List

**Window:** Sat Nov 14, 2026 to Fri Jan 29, 2027
**Hours:** Weeks 1-3 at 6-7h/day. Weeks 4-11 at 3-4h/day (exam mode). On exam-free days, go back to 6h. The day before an exam: 30-60 min recall only.
**Rule for AI use:** never commit code you cannot explain line by line.

---

## Daily routine (tick these every day)

Full load (6-7h):
- [ ] Recall: explain yesterday's topic aloud, 45 min
- [ ] Learn: docs, tutorials, 2.5h
- [ ] Build: apply it in a project, 3h
- [ ] Journal: concepts, mistakes, fixes, 15 min

Exam mode (3-4h):
- [ ] Recall, 30 min
- [ ] Learn, 1h
- [ ] Build, 2h
- [ ] Journal, 15 min

## Weekly routine (last day of each week)

- [ ] Commit and push all work to GitHub
- [ ] Do the week's "Check" items below without notes
- [ ] Review the learning journal and re-read mistakes
- [ ] Re-adjust next week's plan around exam dates
- [ ] Mark the week's boxes in this file

---

## Project MVP checklists

### KajBazar (flagship: React + .NET 8 + EF Core + PostgreSQL + JWT)
- [ ] Repo, README and architecture sketch
- [ ] Database schema and migrations (users, providers, categories, reviews)
- [ ] Auth: register, login, roles (customer, provider, admin)
- [ ] Provider CRUD with ownership checks
- [ ] Search, filter and pagination
- [ ] Reviews and ratings
- [ ] Swagger documentation
- [ ] Tests on critical paths
- [ ] Dockerized
- [ ] Deployed
- [ ] Stretch: near-me search, chef (Babuchii) rates, subscriptions

### Paypulse (React stack lab on a .NET API)
- [ ] Repo, README
- [ ] Vite + React + TypeScript + Tailwind + shadcn/ui set up
- [ ] Employees and departments CRUD
- [ ] Role-based dashboard
- [ ] TanStack Query for all server data
- [ ] One report (e.g. headcount or payroll summary)
- [ ] API with validation and Problem Details
- [ ] Demo and README with screenshots

### Sunshine (security, SignalR and testing lab)
- [ ] Finish core modules (Patient, Doctor, Appointments, Chat, Admin)
- [ ] Security audit (authorization, injection, XSS, CSRF, cookies)
- [ ] Chat hardening with SignalR
- [ ] Integration tests on key flows
- [ ] Dockerized
- [ ] README and ER diagram up to date

### Project 4: production capstone (on KajBazar)
- [ ] Unit and integration tests in CI
- [ ] Docker Compose environment
- [ ] CI/CD pipeline
- [ ] Deployed with domain and HTTPS
- [ ] Backup and restore test
- [ ] Simple load test
- [ ] Threat model
- [ ] Decision records for key trade-offs

---

# PHASE 1: Foundations (Weeks 1-3, full load)

## Week 1 (Nov 14-20): Web and frontend core

**Learn**
- [ ] How a URL becomes a rendered page (DNS, TCP, TLS, HTTP)
- [ ] HTTP methods, headers, status codes, cookies, caching
- [ ] Browser DevTools: Network tab, Elements, Console
- [ ] curl for requests and debugging
- [ ] Linux shell: navigation, pipes, grep, find, permissions
- [ ] Git: branches, merge, conflicts, pull requests, .gitignore
- [ ] Semantic HTML and accessible forms
- [ ] CSS: box model, Flexbox, Grid, mobile-first media queries
- [ ] JavaScript ES6+: let/const, arrow functions, destructuring, modules
- [ ] Closures, event loop, promises, async/await
- [ ] Fetch API and error handling
- [ ] TypeScript: types, interfaces, unions, generics, narrowing

**Build**
- [ ] Responsive page that fetches a public API and handles loading and error states
- [ ] Push it to GitHub using a branch and pull request

**Check**
- [ ] Explain, without notes, what happens from entering a URL to a rendered page
- [ ] Explain the difference between `==` and `===`, and between a promise and async/await

**AI practice**
- [ ] Use AI as a tutor only: write code first, then ask for critique
- [ ] Ask AI "what breaks if I remove this line?" on three snippets

## Week 2 (Nov 21-27): React ecosystem

**Learn**
- [ ] Vite project setup and folder structure
- [ ] React components, props, state
- [ ] Hooks: useState, useEffect, useMemo, useCallback, custom hooks
- [ ] TypeScript in React (props, events, generics)
- [ ] React Router: routes, nested routes, params, protected routes (UI only)
- [ ] Tailwind CSS: utilities, responsive variants, dark mode
- [ ] shadcn/ui: install, components, theming
- [ ] TanStack Query: queries, mutations, caching, invalidation
- [ ] Forms and validation
- [ ] ESLint and Prettier setup

**Build**
- [ ] Paypulse frontend with mock data: layout, sidebar, employee list, detail page
- [ ] Loading, empty and error states on every page
- [ ] Search and pagination in the UI

**Check**
- [ ] Explain server state vs UI state and where TanStack Query fits
- [ ] Explain why a protected route in the UI is not real authorization

**AI practice**
- [ ] Have AI generate one component, then review it for unnecessary state and effects
- [ ] Rewrite one AI-generated component more simply

## Week 3 (Nov 28-Dec 4): API and database

**Learn**
- [ ] ASP.NET Core Web API: controllers vs minimal APIs
- [ ] Middleware pipeline and request flow
- [ ] Dependency injection lifetimes (transient, scoped, singleton)
- [ ] DTOs and why entities are not returned directly
- [ ] Validation and Problem Details error responses
- [ ] Swagger / OpenAPI
- [ ] Configuration by environment and user secrets
- [ ] EF Core: DbContext, entities, relationships, migrations
- [ ] Tracking vs no-tracking queries, N+1 problem, projection to DTOs
- [ ] LINQ revision
- [ ] PostgreSQL: constraints, normalization (1NF-3NF), joins, indexes, transactions
- [ ] Reading a query plan with EXPLAIN
- [ ] Bruno or Postman collections

**Build**
- [ ] Paypulse API: employees and departments with validation
- [ ] Connect the Paypulse frontend to the real API with TanStack Query
- [ ] Add at least two indexes and show the plan before and after

**Check**
- [ ] Explain one index and why it helped
- [ ] Explain scoped vs singleton with an example

**AI practice**
- [ ] Ask AI to find N+1 queries in your code, then confirm them yourself in the logs

---

# PHASE 2: Depth (Weeks 4-7, exam mode)

## Week 4 (Dec 5-11): Auth and security

**Learn**
- [ ] Authentication vs authorization
- [ ] Password hashing and ASP.NET Core Identity
- [ ] Cookies vs JWT: trade-offs, expiry, refresh tokens
- [ ] Roles and policy-based authorization
- [ ] IDOR and object-level authorization
- [ ] OWASP Top 10: injection, XSS, CSRF, broken access control
- [ ] Secure cookie flags: HttpOnly, Secure, SameSite
- [ ] CORS purpose and correct setup

**Build**
- [ ] KajBazar: register, login, roles, protected endpoints
- [ ] Sunshine: security review of auth, cookies and authorization
- [ ] Write a short security checklist for your projects

**Check**
- [ ] Break your own endpoint using another user's ID, then fix it
- [ ] Explain why you never trust the frontend for permissions

**AI practice**
- [ ] Ask AI to review your auth code for missing checks, hardcoded secrets and mass assignment, then verify each claim

## Week 5 (Dec 12-18): Testing and architecture

**Learn**
- [ ] xUnit: arrange-act-assert, theories, fixtures
- [ ] Integration tests with WebApplicationFactory and a test database
- [ ] Playwright: 2-3 end-to-end flows
- [ ] Bruno/Postman collection as a smoke test
- [ ] SOLID principles with examples from your code
- [ ] Clean Architecture basics: dependency direction, separating API, application and infrastructure

**Build**
- [ ] Tests for KajBazar's critical paths (auth, provider CRUD, reviews)
- [ ] Authorization tests (user A cannot touch user B's data)
- [ ] Refactor one KajBazar module toward cleaner layers

**Check**
- [ ] Write a regression test for a bug you fix
- [ ] Explain what makes a test useful rather than just adding coverage

**AI practice**
- [ ] You list the test cases first, then let AI write the code; review that assertions are meaningful

## Week 6 (Dec 19-25): Real-time, caching, data

**Learn**
- [ ] SignalR: hubs, groups, authentication on hubs
- [ ] Redis basics: strings, hashes, TTL
- [ ] Cache-aside pattern and invalidation
- [ ] Pagination and filtering done correctly (server-side)
- [ ] MySQL vs PostgreSQL differences (2-3h only)

**Build**
- [ ] Sunshine chat hardening (auth on hub, input limits, message validation)
- [ ] KajBazar search and reviews with pagination
- [ ] Cache one read-heavy KajBazar endpoint with Redis

**Check**
- [ ] Explain what happens on a cache miss and on invalidation
- [ ] Explain stale data risk with a concrete example

**AI practice**
- [ ] Write a spec for one feature (inputs, outputs, edge cases) before asking an agent to build it
- [ ] Add a project rules file listing your conventions

## Week 7 (Dec 26-Jan 1): Containers

**Learn**
- [ ] Linux server basics: users, permissions, services, logs
- [ ] SSH keys and secure access
- [ ] Docker: images, containers, layers, volumes, networks
- [ ] Multi-stage Dockerfile for .NET and for a React build
- [ ] Docker Compose for API + PostgreSQL + Redis + frontend
- [ ] Nginx as reverse proxy
- [ ] Keeping secrets out of images and Git

**Build**
- [ ] Dockerize KajBazar and Sunshine
- [ ] Compose file with health checks and restart policies
- [ ] Run containers as non-root where possible

**Check**
- [ ] A fresh clone runs with one command
- [ ] Explain image vs container and why volumes matter

**AI practice**
- [ ] Use an agent for the Compose file, then explain every line back

---

# PHASE 3: Ship and design (Weeks 8-11)

## Week 8 (Jan 2-8): CI/CD and hardening

**Learn**
- [ ] GitHub Actions: workflows, jobs, secrets, caching
- [ ] Build, test and lint pipeline
- [ ] Building and publishing a Docker image
- [ ] Deploying to a VPS over SSH
- [ ] Cloudflare: DNS records, proxy, TLS
- [ ] Rate limiting, security headers, CORS tightening
- [ ] Secrets handling in CI and in production

**Build**
- [ ] CI pipeline for KajBazar
- [ ] Deploy KajBazar with a domain and HTTPS
- [ ] Add health check endpoint

**Check**
- [ ] The pipeline fails on a broken test and blocks the merge
- [ ] You can redeploy and roll back

**AI practice**
- [ ] Add AI review on pull requests and compare its findings with your own review

## Week 9 (Jan 9-15): Project finish line

No new topics this week. Cut scope, not quality.

- [ ] KajBazar: all MVP items done
- [ ] Paypulse: all MVP items done
- [ ] Sunshine: all MVP items done
- [ ] README for each project: setup steps, screenshots, architecture, trade-offs
- [ ] ER diagram for each project
- [ ] Short demo run-through for each project
- [ ] Another person can clone and run each project

## Week 10 (Jan 16-22): System design

**Learn**
- [ ] Functional vs non-functional requirements
- [ ] Back-of-envelope estimates: requests, storage, bandwidth
- [ ] Caching layers: browser, CDN, application, database
- [ ] Load balancing, stateless services, horizontal scaling
- [ ] Queues and background jobs (concept only)
- [ ] Failure modes, retries, timeouts, idempotency

**Do**
- [ ] Design a URL shortener (short design doc)
- [ ] Design a booking system, including double-booking prevention
- [ ] Design a chat system
- [ ] Design a notification service
- [ ] Threat-model KajBazar (assets, entry points, abuse cases)

**Check**
- [ ] For each design, name the bottleneck and one failure mode

## Week 11 (Jan 23-29): Capstone and review

- [ ] Backup and restore test on KajBazar's database
- [ ] Simple load test and a short results note
- [ ] Decision records for 3-5 key trade-offs
- [ ] Update threat model after fixes
- [ ] No-AI explain-back: walk through your KajBazar request flow from browser to database without notes
- [ ] Answer the Completion Review questions below
- [ ] Log your gaps and pick the first advanced topic

---

## Completion Review (answer without notes)

- [ ] Can I trace a browser request from DNS through HTTPS, the API, application logic and the database?
- [ ] Can I design a relational schema and explain constraints and indexes?
- [ ] Can I build and test an API with validation, authentication, authorization and consistent errors?
- [ ] Can I build a responsive frontend with loading, empty, success and failure states?
- [ ] Can I debug using logs, browser tools, a debugger and query plans?
- [ ] Can I deploy and safely manage configuration, secrets, backups and migrations?
- [ ] Can I identify likely security vulnerabilities and test access controls?
- [ ] Can I explain behavior during a database outage or traffic spike?
- [ ] Can I justify architecture choices with requirements and trade-offs?
- [ ] Can another developer clone my project and run it from my documentation?

---

## Deliberately kept shallow

- MySQL: comparison with PostgreSQL only
- Redis: caching only
- Cloudflare: DNS and proxy only
- Playwright: a few critical flows
- Clean Architecture: principles, not ceremony
- SignalR: one real feature

## Advanced backlog (after Week 11)

- [ ] Architecture: microservices, CQRS, event sourcing, DDD in depth, multi-tenancy
- [ ] Messaging: RabbitMQ or Kafka, sagas, outbox pattern
- [ ] Infrastructure: Kubernetes, Terraform, a cloud provider's core services
- [ ] Security: OAuth2/OIDC with Keycloak, penetration testing with Burp, WAF and CDN
- [ ] Data and observability: Postgres partitioning, replication and MVCC tuning, PostGIS, OpenTelemetry, Prometheus, Grafana, k6
- [ ] Frontend: Next.js and SSR, advanced React performance, Core Web Vitals