# Full-Stack Development & System Design --- Learning Roadmap

A practical, checkbox-based roadmap from fundamentals to advanced
engineering. Work through the sections in order, but build small
projects throughout the journey rather than waiting until the end.

**Suggested primary stack:** HTML, CSS, JavaScript, TypeScript, ASP.NET
Core Web API, C#, Entity Framework Core, PostgreSQL or MySQL, Git,
Linux, Docker, and a cloud platform. Concepts transfer to other stacks.

**How to use this checklist** - \[ \] Learn the concept and explain it
in your own words. - \[ \] Implement it in a small exercise or
project. - \[ \] Test it and document what you learned. - \[ \] Revisit
difficult topics after building a real application.

------------------------------------------------------------------------

## 0. Learning Habits & Developer Workflow

-   [x] Set a realistic weekly learning schedule.
-   [x] Learn to read official documentation and error messages.
-   [x] Break large tasks into small, testable steps.
-   [x] Keep a learning journal with concepts, mistakes, and fixes.
-   [x] Learn to ask useful technical questions and provide reproducible
    examples.
-   [x] Practice debugging before searching for a complete solution.
-   [x] Use spaced repetition for important concepts.
-   [x] Learn to estimate tasks and record what took longer than
    expected.
-   [x] Write clear README files and setup instructions.
-   [x] Learn to distinguish a quick prototype from production-ready
    software.

## 1. Computer, Internet & Command-Line Fundamentals

### Computer and operating-system basics

-   [x] Understand CPU, RAM, storage, processes, and threads.
-   [x] Understand binary, bits, bytes, and common data-size units.
-   [ ] Understand files, directories, paths, permissions, and
    environment variables.
-   [ ] Understand processes, signals, services, and logs.
-   [ ] Understand memory use, CPU use, disk I/O, and basic resource
    monitoring.
-   [ ] Learn Linux terminal navigation and file operations.
-   [ ] Learn pipes, redirection, grep, find, sed, awk, and command
    chaining.
-   [ ] Learn shell scripting basics.
-   [ ] Understand package managers and application installation.
-   [ ] Learn SSH, keys, remote shells, and secure file transfer.

### Networking and the Internet

-   [x] Understand client-server architecture.
-   [ ] Understand LAN, WAN, routers, switches, and NAT at a high level.
-   [ ] Understand IP addresses, ports, TCP, UDP, and sockets.
-   [ ] Understand DNS resolution and DNS records.
-   [ ] Understand domain names, registrars, and hosting.
-   [ ] Understand HTTP requests and responses.
-   [ ] Understand methods, headers, status codes, and message bodies.
-   [ ] Understand HTTPS, TLS certificates, encryption, and certificate
    validation.
-   [ ] Understand cookies, sessions, cache, and browser storage.
-   [ ] Understand proxies, reverse proxies, and CDNs.
-   [ ] Use browser DevTools Network tab to inspect requests.
-   [ ] Use curl to make and debug HTTP requests.
-   [ ] Explain what happens from entering a URL to rendering a web
    page.

**Milestone project:** Serve a static website locally, inspect its
network requests, and explain its DNS/HTTP journey.

## 2. Programming Foundations

### Core programming

-   [ ] Variables, constants, primitive types, and type conversion.
-   [ ] Operators, expressions, and precedence.
-   [ ] Conditional logic and loops.
-   [ ] Functions, parameters, return values, and scope.
-   [ ] Arrays, strings, collections, and iteration.
-   [ ] Input/output and file handling.
-   [ ] Error handling and exceptions.
-   [ ] Modules, namespaces, packages, and imports.
-   [ ] Debugging with breakpoints and a debugger.
-   [ ] Write readable names and small, focused functions.
-   [ ] Learn basic testing and edge-case thinking.

### Data structures and algorithms

-   [ ] Big-O time and space complexity.
-   [ ] Arrays and dynamic arrays.
-   [ ] Linked lists.
-   [ ] Stacks and queues.
-   [ ] Hash maps and sets.
-   [ ] Trees and binary search trees.
-   [ ] Heaps and priority queues.
-   [ ] Graphs and graph representations.
-   [ ] Recursion and backtracking.
-   [ ] Linear and binary search.
-   [ ] Sorting algorithms and their trade-offs.
-   [ ] Two pointers and sliding window.
-   [ ] Prefix sums and difference arrays.
-   [ ] Breadth-first search and depth-first search.
-   [ ] Greedy algorithms.
-   [ ] Divide and conquer.
-   [ ] Dynamic programming fundamentals.
-   [ ] Practice solving problems without immediately viewing solutions.
-   [ ] Compare a standard-library implementation with a manual
    implementation.

### Object-oriented and maintainable code

-   [ ] Classes, objects, fields, properties, and methods.
-   [ ] Constructors and object lifecycle.
-   [ ] Encapsulation and access modifiers.
-   [ ] Abstraction and interfaces.
-   [ ] Inheritance and composition.
-   [ ] Polymorphism and method overriding.
-   [ ] Value types vs reference types (where applicable).
-   [ ] Generics and reusable abstractions.
-   [ ] Immutability and side effects.
-   [ ] SOLID principles and when not to over-apply them.
-   [ ] Common design patterns: Strategy, Factory, Adapter, Decorator,
    Observer, Repository.
-   [ ] Refactoring and code smells.
-   [ ] Separate business logic from input/output and framework code.

**Milestone project:** Build a command-line application with multiple
classes, validation, file persistence, tests, and a clear README.

## 3. Git, Collaboration & Engineering Workflow

-   [ ] Initialize repositories and understand the working tree, staging
    area, and commits.
-   [ ] Use status, diff, log, add, commit, restore, and reset safely.
-   [ ] Create branches and merge changes.
-   [ ] Resolve merge conflicts.
-   [ ] Understand rebase vs merge and avoid rewriting shared history
    carelessly.
-   [ ] Use `.gitignore` and keep secrets out of Git.
-   [ ] Write meaningful commit messages.
-   [ ] Create and review pull requests.
-   [ ] Use issues, labels, milestones, and project boards.
-   [ ] Learn semantic versioning and release tags.
-   [ ] Use code formatting, linting, and pre-commit checks.
-   [ ] Learn code review etiquette and how to respond to review
    feedback.
-   [ ] Create a reproducible development setup.
-   [ ] Understand CI pipelines at a high level.

**Milestone project:** Collaborate on a small application using
branches, pull requests, review, and automated checks.

## 4. Web Frontend --- Beginner to Advanced

### HTML

-   [ ] Semantic HTML elements and document structure.
-   [ ] Headings, links, images, lists, and tables.
-   [ ] Forms, labels, input types, validation, and accessible errors.
-   [ ] Metadata, title, favicon, and social preview basics.
-   [ ] Accessibility basics: semantic structure, keyboard navigation,
    labels, and alt text.
-   [ ] Understand the DOM.

### CSS and responsive design

-   [ ] Selectors, specificity, inheritance, and cascade.
-   [ ] Box model, display, positioning, and stacking context.
-   [ ] Flexbox and CSS Grid.
-   [ ] Typography, colors, spacing, and design tokens.
-   [ ] Pseudo-classes, pseudo-elements, and transitions.
-   [ ] Responsive layouts and mobile-first design.
-   [ ] Media queries and fluid sizing.
-   [ ] Reusable components and consistent design systems.
-   [ ] Focus states, contrast, and reduced-motion preferences.
-   [ ] CSS organization and avoiding unnecessary overrides.
-   [ ] Test layouts across screen sizes.

### JavaScript and TypeScript

-   [ ] Values, types, coercion, equality, and scope.
-   [ ] Functions, closures, and higher-order functions.
-   [ ] Objects, arrays, destructuring, and spread syntax.
-   [ ] Modules and dependency management.
-   [ ] DOM selection, events, and event delegation.
-   [ ] Form validation and user feedback.
-   [ ] Promises, async/await, and error handling.
-   [ ] Fetch API and HTTP error handling.
-   [ ] Event loop, call stack, tasks, and microtasks.
-   [ ] Local storage, session storage, cookies, and their security
    trade-offs.
-   [ ] TypeScript types, interfaces, unions, generics, and narrowing.
-   [ ] Runtime validation of untrusted API data.
-   [ ] Avoid unsafe HTML injection and understand XSS risks.
-   [ ] Learn frontend build tools and package scripts.
-   [ ] Use browser DevTools for debugging and performance analysis.

### Frontend architecture and user experience

-   [ ] Component-based UI architecture.
-   [ ] Reusable components and clear component boundaries.
-   [ ] Props, local state, and shared state.
-   [ ] Forms, loading states, empty states, and error states.
-   [ ] Client-side routing and navigation.
-   [ ] API service layer and consistent error handling.
-   [ ] Authentication UI and protected routes (without relying on UI
    for authorization).
-   [ ] Pagination, filtering, sorting, and search.
-   [ ] Optimistic updates and rollback where appropriate.
-   [ ] Accessibility testing.
-   [ ] Frontend unit and component tests.
-   [ ] End-to-end browser testing.
-   [ ] Performance: code splitting, lazy loading, image optimization,
    and bundle analysis.
-   [ ] SEO basics, metadata, and rendering strategies.
-   [ ] Internationalization and localization.
-   [ ] Understand when vanilla JavaScript is enough and when a
    framework is useful.

**Milestone project:** Build a responsive dashboard that consumes an
API, supports forms/search/pagination, handles loading and errors, and
passes accessibility checks.

## 5. Backend Development with C# and ASP.NET Core

### C# foundations

-   [ ] Types, control flow, methods, classes, and interfaces.
-   [ ] Collections, generics, and LINQ.
-   [ ] Nullable reference types and null safety.
-   [ ] Exceptions and structured error handling.
-   [ ] Delegates, events, lambdas, and extension methods.
-   [ ] Records, enums, and pattern matching.
-   [ ] Async/await, Tasks, cancellation tokens, and exception
    propagation.
-   [ ] Dependency injection concepts.
-   [ ] Configuration and options.
-   [ ] Logging and diagnostics.
-   [ ] Unit testing with a test framework.
-   [ ] Understand disposable resources and
    `IDisposable`/`IAsyncDisposable`.

### HTTP APIs and ASP.NET Core

-   [ ] Understand middleware and the request pipeline.
-   [ ] Routing, controllers, actions, and minimal APIs.
-   [ ] Model binding and input validation.
-   [ ] DTOs and why API contracts should not expose persistence
    entities directly.
-   [ ] Dependency injection lifetimes: transient, scoped, singleton.
-   [ ] Configuration by environment and secret management.
-   [ ] Consistent error responses and Problem Details.
-   [ ] Logging, correlation IDs, and request tracing.
-   [ ] OpenAPI/Swagger documentation.
-   [ ] Pagination, filtering, sorting, and search.
-   [ ] API versioning strategy.
-   [ ] File upload/download limits and validation.
-   [ ] Background services and scheduled jobs.
-   [ ] Health checks and readiness checks.
-   [ ] Rate limiting and request-size limits.
-   [ ] CORS and its correct purpose.
-   [ ] Cancellation and timeouts.
-   [ ] Graceful shutdown.
-   [ ] SignalR or WebSockets for real-time requirements.
-   [ ] Generate useful API documentation and examples.

### Backend architecture

-   [ ] Separate API, application/business logic, and infrastructure
    concerns.
-   [ ] Understand layered architecture.
-   [ ] Understand Clean Architecture and dependency direction.
-   [ ] Understand modular monoliths and bounded contexts.
-   [ ] Use interfaces where they create useful boundaries, not
    everywhere.
-   [ ] Transaction boundaries and unit-of-work concepts.
-   [ ] Domain validation and business invariants.
-   [ ] Avoid putting all logic into controllers.
-   [ ] Avoid unnecessary generic repositories over an ORM.
-   [ ] Handle concurrency and duplicate requests.
-   [ ] Design stable API contracts.
-   [ ] Use feature folders or modules consistently.
-   [ ] Understand when a monolith is preferable to microservices.

**Milestone project:** Build a versioned REST API with validation,
authentication, authorization, persistence, logs, tests, and OpenAPI
documentation.

## 6. Databases, SQL & Data Modeling

### Relational database foundations

-   [ ] Tables, rows, columns, data types, and constraints.
-   [ ] Primary keys, foreign keys, unique constraints, and checks.
-   [ ] One-to-one, one-to-many, and many-to-many relationships.
-   [ ] ER diagrams and cardinality.
-   [ ] Normalization: 1NF, 2NF, 3NF, and BCNF.
-   [ ] Denormalization and its trade-offs.
-   [ ] INSERT, SELECT, UPDATE, and DELETE.
-   [ ] WHERE, ORDER BY, GROUP BY, HAVING, and aggregate functions.
-   [ ] Joins, subqueries, CTEs, and set operations.
-   [ ] Views and materialized views where supported.
-   [ ] Transactions and ACID properties.
-   [ ] Isolation levels, locks, and deadlocks.
-   [ ] Indexes: B-tree and other common index types.
-   [ ] Read execution plans and identify expensive queries.
-   [ ] Composite indexes and column order.
-   [ ] Triggers, stored procedures, and generated columns where
    appropriate.
-   [ ] Migrations and schema evolution.
-   [ ] Seed data and repeatable database setup.
-   [ ] Backups, restores, and recovery testing.
-   [ ] Database users, privileges, and least privilege.
-   [ ] SQL injection prevention with parameterized queries.
-   [ ] Understand OLTP vs OLAP.

### ORM and application data access

-   [ ] Entity Framework Core entities and `DbContext`.
-   [ ] Relationships and navigation properties.
-   [ ] Migrations and migration review.
-   [ ] Tracking vs no-tracking queries.
-   [ ] Eager, explicit, and lazy loading trade-offs.
-   [ ] Avoid N+1 query problems.
-   [ ] Projection to DTOs and selecting only required columns.
-   [ ] Transactions and concurrency tokens.
-   [ ] Connection pooling and resource disposal.
-   [ ] Testing against a realistic database engine.
-   [ ] Understand when raw SQL is useful.
-   [ ] Manage development, test, and production schemas safely.

### NoSQL and specialized storage

-   [ ] Understand document, key-value, wide-column, and graph
    databases.
-   [ ] Compare relational and document data modeling.
-   [ ] Understand Redis use cases and cache data structures.
-   [ ] Understand object storage for uploaded files and media.
-   [ ] Understand search indexes and full-text search.
-   [ ] Choose storage based on access patterns and consistency needs.

**Milestone project:** Design and implement a normalized database for a
real workflow; document the ERD, constraints, indexes, and important
queries.

## 7. Authentication, Authorization & Application Security

-   [ ] Authentication vs authorization.
-   [ ] Password hashing with a modern password-hashing algorithm.
-   [ ] Secure registration, login, logout, and password reset flows.
-   [ ] Cookies vs bearer tokens and their trade-offs.
-   [ ] Sessions, token expiry, refresh, revocation, and rotation.
-   [ ] OAuth 2.0 and OpenID Connect concepts.
-   [ ] Multi-factor authentication concepts.
-   [ ] Role-based and policy-based authorization.
-   [ ] Enforce permissions on the server for every protected operation.
-   [ ] Object-level authorization and IDOR prevention.
-   [ ] CSRF, XSS, SQL injection, SSRF, and command injection.
-   [ ] Input validation, output encoding, and safe serialization.
-   [ ] Secure cookie flags: HttpOnly, Secure, and SameSite.
-   [ ] TLS, secret storage, and key rotation.
-   [ ] Rate limiting, brute-force protection, and abuse detection.
-   [ ] CORS policy and security headers.
-   [ ] File upload validation, storage isolation, and malware
    considerations.
-   [ ] Dependency vulnerability scanning and updates.
-   [ ] Threat modeling and attack-surface review.
-   [ ] Audit logs for sensitive operations without logging secrets.
-   [ ] Data minimization, retention, and privacy.
-   [ ] Learn the OWASP Top 10 and test against relevant risks.
-   [ ] Create a security checklist for releases.

**Milestone project:** Threat-model an application and test
authorization, input validation, session/token handling, and common web
vulnerabilities.

## 8. Testing & Quality Engineering

-   [ ] Unit tests for pure business logic.
-   [ ] Integration tests for database and API behavior.
-   [ ] End-to-end tests for critical user journeys.
-   [ ] Test doubles, mocks, fakes, and when to use each.
-   [ ] Arrange-Act-Assert and readable test names.
-   [ ] Test validation, edge cases, and failure paths.
-   [ ] Test authorization boundaries.
-   [ ] Test database constraints and transactions.
-   [ ] Test background jobs and retry behavior.
-   [ ] Test API contracts and backward compatibility.
-   [ ] Use deterministic test data and isolate tests.
-   [ ] Avoid tests that depend on execution order.
-   [ ] Measure coverage without treating coverage as proof of quality.
-   [ ] Add regression tests for fixed bugs.
-   [ ] Perform smoke tests after deployment.
-   [ ] Learn load, stress, and soak testing.
-   [ ] Use static analysis, formatters, and dependency scanners.
-   [ ] Add tests to CI and make failures actionable.

## 9. Software Design & System Design Foundations

### Requirements and design thinking

-   [ ] Identify users, goals, workflows, and system boundaries.
-   [ ] Gather functional requirements.
-   [ ] Define non-functional requirements: latency, availability,
    durability, security, and cost.
-   [ ] Convert vague requirements into measurable acceptance criteria.
-   [ ] Estimate traffic, data volume, storage, and bandwidth.
-   [ ] Define assumptions explicitly.
-   [ ] Identify constraints and trade-offs.
-   [ ] Draw context diagrams and container/component diagrams.
-   [ ] Model key entities and their relationships.
-   [ ] Document API contracts and sequence diagrams.
-   [ ] Identify failure modes and recovery behavior.
-   [ ] Explain why a design is appropriate for its expected scale.

### Core architecture concepts

-   [ ] Client-server and three-tier architecture.
-   [ ] Monolith, modular monolith, and microservices.
-   [ ] Layered, hexagonal, and Clean Architecture.
-   [ ] Domain-Driven Design fundamentals: entities, value objects,
    aggregates, bounded contexts.
-   [ ] Synchronous vs asynchronous communication.
-   [ ] REST, RPC, and event-driven communication.
-   [ ] Strong consistency vs eventual consistency.
-   [ ] Stateless vs stateful services.
-   [ ] Coupling, cohesion, and dependency direction.
-   [ ] Architecture Decision Records (ADRs).
-   [ ] Apply design patterns to real problems rather than by habit.

### Scalability and reliability

-   [ ] Vertical vs horizontal scaling.
-   [ ] Stateless application servers and load balancing.
-   [ ] Reverse proxies and API gateways.
-   [ ] Caching: browser, CDN, application, and database layers.
-   [ ] Cache-aside, write-through, and write-behind patterns.
-   [ ] TTLs, invalidation, stale data, and cache stampedes.
-   [ ] Database indexing, query optimization, and connection pooling.
-   [ ] Read replicas and their consistency trade-offs.
-   [ ] Database partitioning and sharding concepts.
-   [ ] Replication and failover.
-   [ ] Queues, streams, and asynchronous processing.
-   [ ] Retries with backoff and jitter.
-   [ ] Timeouts, circuit breakers, and bulkheads.
-   [ ] Idempotency and deduplication.
-   [ ] Rate limiting, quotas, and load shedding.
-   [ ] Graceful degradation and backpressure.
-   [ ] Single points of failure and redundancy.
-   [ ] Availability, reliability, durability, and fault tolerance.
-   [ ] Recovery objectives: RTO and RPO.
-   [ ] CAP theorem and its practical limits.
-   [ ] Understand the trade-offs of distributed transactions.
-   [ ] Sagas, outbox pattern, and compensating actions.
-   [ ] Exactly-once claims vs at-least-once delivery and idempotent
    handling.

### System design interview practice

-   [ ] Clarify requirements and scope before drawing boxes.
-   [ ] Define APIs and data models.
-   [ ] Estimate request rate, storage growth, and bandwidth.
-   [ ] Draw a high-level architecture.
-   [ ] Identify bottlenecks and failure points.
-   [ ] Explain trade-offs and alternatives.
-   [ ] Design for observability and operational ownership.
-   [ ] Practice a URL shortener.
-   [ ] Practice a file storage and sharing service.
-   [ ] Practice a notification service.
-   [ ] Practice a chat or real-time messaging system.
-   [ ] Practice a news feed.
-   [ ] Practice an e-commerce checkout.
-   [ ] Practice a booking/reservation system.
-   [ ] Practice a video or media delivery platform.
-   [ ] Practice a rate limiter.
-   [ ] Practice a search/autocomplete service.
-   [ ] Write a short design document after each exercise.

## 10. Caching, Messaging & Distributed Systems

-   [ ] Understand why caches work and when they do not.
-   [ ] Cache keys, TTLs, eviction policies, and memory limits.
-   [ ] Redis data structures and atomic operations.
-   [ ] Cache invalidation strategies and stale reads.
-   [ ] Message queues vs event streams.
-   [ ] Producers, consumers, partitions, offsets, and consumer groups.
-   [ ] At-most-once, at-least-once, and effectively-once processing.
-   [ ] Dead-letter queues and poison messages.
-   [ ] Retry policies and duplicate delivery.
-   [ ] Idempotent consumers.
-   [ ] Event-driven architecture and domain events.
-   [ ] Event sourcing concepts and trade-offs.
-   [ ] CQRS concepts and when not to use it.
-   [ ] Transactional outbox and inbox patterns.
-   [ ] Schema evolution and event versioning.
-   [ ] Service discovery and configuration distribution.
-   [ ] Distributed locks and their hazards.
-   [ ] Clock skew, ordering, and distributed coordination basics.
-   [ ] Consensus concepts at a high level.
-   [ ] Know when a single database and background worker are
    sufficient.

## 11. DevOps, Containers & Deployment

### Linux and runtime operations

-   [ ] Run applications as services.
-   [ ] Configure environment variables and secrets.
-   [ ] Read application and system logs.
-   [ ] Configure file permissions and service users.
-   [ ] Understand ports, firewalls, and reverse proxy configuration.
-   [ ] Configure HTTPS and renew certificates.
-   [ ] Diagnose process, memory, disk, and network issues.
-   [ ] Understand DNS changes and propagation at a practical level.

### Docker and deployment

-   [ ] Understand images, containers, registries, and layers.
-   [ ] Write a Dockerfile for a web API.
-   [ ] Use multi-stage builds.
-   [ ] Run a database and API locally with Docker Compose.
-   [ ] Use volumes and understand persistence.
-   [ ] Configure networks, ports, health checks, and restart policies.
-   [ ] Keep secrets out of images and source control.
-   [ ] Run containers as non-root where feasible.
-   [ ] Understand container resource limits.
-   [ ] Build repeatable development and production images.
-   [ ] Deploy behind a reverse proxy.
-   [ ] Configure domain, DNS, and TLS.
-   [ ] Use separate development, staging, and production environments.
-   [ ] Perform safe database migrations during release.
-   [ ] Implement rollback and recovery procedures.

### CI/CD and infrastructure

-   [ ] Build, test, and lint automatically on each change.
-   [ ] Build and publish versioned artifacts/images.
-   [ ] Use deployment approvals for high-risk environments.
-   [ ] Manage secrets in CI securely.
-   [ ] Learn deployment strategies: rolling, blue-green, and canary.
-   [ ] Understand infrastructure as code.
-   [ ] Learn one cloud provider's core concepts: compute, networking,
    storage, identity, and managed databases.
-   [ ] Understand cost monitoring, budgets, and resource cleanup.
-   [ ] Create a disaster recovery and backup plan.
-   [ ] Practice restoring a backup rather than merely creating one.

## 12. Observability, Performance & Production Readiness

-   [ ] Structured logging with useful context.
-   [ ] Metrics, logs, traces, and their different purposes.
-   [ ] Correlation and trace IDs across services.
-   [ ] Define SLIs, SLOs, and error budgets.
-   [ ] Monitor latency percentiles, throughput, errors, and saturation.
-   [ ] Create useful health and readiness checks.
-   [ ] Set actionable alerts and reduce alert noise.
-   [ ] Profile CPU, memory, allocations, database queries, and network
    latency.
-   [ ] Use load testing to find bottlenecks.
-   [ ] Establish performance budgets.
-   [ ] Diagnose slow endpoints using traces and query plans.
-   [ ] Understand queue depth, consumer lag, and retry rates.
-   [ ] Create runbooks for common incidents.
-   [ ] Conduct incident reviews focused on learning and prevention.
-   [ ] Define backup verification, recovery tests, and retention.
-   [ ] Review cost, security, reliability, and operational burden
    before launch.

## 13. Advanced Backend & API Engineering

-   [ ] API design consistency and compatibility.
-   [ ] Idempotency keys for payment/order-like operations.
-   [ ] Webhooks: signature validation, retries, and deduplication.
-   [ ] Background job scheduling and reliable execution.
-   [ ] Large file upload/download and streaming.
-   [ ] Real-time updates with WebSockets or SignalR.
-   [ ] Multi-tenant architecture and tenant isolation.
-   [ ] Auditability and append-only event records where needed.
-   [ ] Data export and import pipelines.
-   [ ] Search indexing and eventual consistency.
-   [ ] API quotas and usage-based limits.
-   [ ] Graceful handling of third-party outages.
-   [ ] External integration adapters and contract tests.
-   [ ] Data retention and deletion workflows.
-   [ ] Secure handling of personally identifiable and sensitive data.
-   [ ] Evaluate resilience, latency, and cost for every major
    dependency.

## 14. Advanced Frontend Engineering

-   [ ] Type-safe API integration.
-   [ ] Shared design system and component conventions.
-   [ ] State management based on actual complexity.
-   [ ] Server state vs client UI state.
-   [ ] Form schemas and validation.
-   [ ] Error boundaries and recovery UX where supported.
-   [ ] Route-level code splitting and lazy loading.
-   [ ] Core Web Vitals and real-user performance measurement.
-   [ ] Accessibility audit and keyboard-only navigation.
-   [ ] Security review of rendering and browser storage.
-   [ ] Content Security Policy concepts.
-   [ ] Cross-browser testing.
-   [ ] Offline behavior and service worker basics when appropriate.
-   [ ] Internationalization, locale formatting, and right-to-left
    support if required.
-   [ ] Frontend telemetry and privacy-aware analytics.
-   [ ] Visual regression testing for critical UI.
-   [ ] Avoid premature abstraction and excessive global state.

## 15. Architecture at Larger Scale

-   [ ] Identify domain boundaries before splitting services.
-   [ ] Understand the cost of network calls between services.
-   [ ] Service ownership and independent deployment.
-   [ ] API gateway vs service mesh responsibilities.
-   [ ] Centralized vs decentralized configuration.
-   [ ] Distributed tracing across services.
-   [ ] Service-to-service identity and authorization.
-   [ ] Resilience policies and failure isolation.
-   [ ] Data ownership per service.
-   [ ] Cross-service workflows and saga orchestration/choreography.
-   [ ] Event schema governance and compatibility.
-   [ ] Read models and data replication.
-   [ ] Multi-region architecture and replication trade-offs.
-   [ ] Disaster recovery across regions.
-   [ ] Capacity planning and autoscaling.
-   [ ] Cost allocation and cloud resource governance.
-   [ ] Understand Kubernetes fundamentals before adopting it.
-   [ ] Learn containers, pods, deployments, services, ingress,
    configuration, and secrets in Kubernetes.
-   [ ] Understand the operational cost of microservices and Kubernetes.
-   [ ] Evaluate whether a modular monolith is simpler and safer.

## 16. Advanced Data Engineering & Database Performance

-   [ ] Read execution plans and benchmark changes.
-   [ ] Understand index selectivity and write overhead.
-   [ ] Tune connection pools and transaction duration.
-   [ ] Diagnose locks and deadlocks.
-   [ ] Understand MVCC and database isolation.
-   [ ] Partition large tables based on query and retention patterns.
-   [ ] Understand replication lag and read-after-write needs.
-   [ ] Design archival and retention strategies.
-   [ ] Use bulk operations for large imports.
-   [ ] Design safe schema migrations for live systems.
-   [ ] Understand CDC (change data capture) concepts.
-   [ ] Understand analytical warehouses and data pipelines.
-   [ ] Distinguish operational databases from analytical systems.
-   [ ] Measure before and after every performance optimization.

## 17. Professional Practice & Technical Leadership

-   [ ] Write technical proposals and design documents.
-   [ ] Explain architecture to technical and non-technical audiences.
-   [ ] Review pull requests for correctness, security, and
    maintainability.
-   [ ] Mentor through explanation and constructive feedback.
-   [ ] Break down epics into deliverable tasks.
-   [ ] Make trade-offs explicit and document important decisions.
-   [ ] Plan migrations and deprecations.
-   [ ] Manage technical debt intentionally.
-   [ ] Estimate work with uncertainty and dependencies in mind.
-   [ ] Communicate risks early.
-   [ ] Run blameless incident reviews.
-   [ ] Evaluate libraries and frameworks by maintenance, security, fit,
    and cost.
-   [ ] Keep learning through documentation, experiments, and
    postmortems.

------------------------------------------------------------------------

# Portfolio Projects --- Apply the Topics

Complete projects in increasing complexity. Each project should include
a README, architecture diagram, database design where relevant, tests,
setup instructions, and a short explanation of trade-offs.

## Project 1 --- Responsive Personal Website

-   [ ] Semantic HTML and accessible CSS.
-   [ ] Responsive mobile-first layout.
-   [ ] Contact form with validation.
-   [ ] Deployment with a custom domain if available.
-   [ ] Basic performance and accessibility checks.

## Project 2 --- Task Manager

-   [ ] CRUD operations and input validation.
-   [ ] Relational schema and migrations.
-   [ ] REST API and DTOs.
-   [ ] Unit and integration tests.
-   [ ] Filtering, sorting, and pagination.
-   [ ] Error handling and API documentation.

## Project 3 --- Authentication and Role-Based Portal

-   [ ] Registration, login, logout, and password reset flow.
-   [ ] Secure password hashing and session/token handling.
-   [ ] Roles and policy-based authorization.
-   [ ] Object-level permission tests.
-   [ ] Audit events for sensitive actions.
-   [ ] Threat model and security checklist.

## Project 4 --- E-Commerce or Pharmacy Inventory System

-   [ ] Products, categories, suppliers, customers, and stock.
-   [ ] Purchase and sales workflows.
-   [ ] Transactions that preserve inventory correctness.
-   [ ] Role-based access and audit logs.
-   [ ] Expiry/low-stock alerts where relevant.
-   [ ] Search, pagination, and reporting.
-   [ ] Idempotent order/payment workflow simulation.
-   [ ] Integration and end-to-end tests.

## Project 5 --- Appointment or Booking Platform

-   [ ] Availability and booking rules.
-   [ ] Prevent double-booking under concurrent requests.
-   [ ] Notifications and background jobs.
-   [ ] Cancellation and rescheduling.
-   [ ] Audit trail and time-zone handling.
-   [ ] Load-test the booking endpoint.
-   [ ] Document consistency and transaction decisions.

## Project 6 --- Production-Ready Full-Stack Application

-   [ ] Clear frontend, backend, and database boundaries.
-   [ ] Docker Compose development environment.
-   [ ] CI pipeline for formatting, tests, and builds.
-   [ ] Secure configuration and secret management.
-   [ ] Structured logs, metrics, and health checks.
-   [ ] Deployment, HTTPS, backups, and restore test.
-   [ ] Load test and performance report.
-   [ ] Threat model and operational runbook.
-   [ ] Architecture Decision Records for important trade-offs.

## Project 7 --- Distributed-System Design Exercise

-   [ ] Design a notification, chat, feed, or file-sharing service.
-   [ ] Define measurable functional and non-functional requirements.
-   [ ] Estimate traffic and storage.
-   [ ] Draw architecture, data flow, and sequence diagrams.
-   [ ] Identify failure modes and bottlenecks.
-   [ ] Design retries, idempotency, monitoring, and recovery.
-   [ ] Compare a simple design with a scaled-out alternative.
-   [ ] Explain when additional infrastructure becomes justified.

------------------------------------------------------------------------

# Suggested Learning Order

1.  [ ] Internet, Linux, programming fundamentals, and Git.
2.  [ ] HTML, CSS, JavaScript, SQL, and basic data structures.
3.  [ ] C# and object-oriented programming.
4.  [ ] ASP.NET Core APIs and relational database design.
5.  [ ] Frontend API integration and responsive UI.
6.  [ ] Authentication, authorization, and testing.
7.  [ ] Build and deploy a complete CRUD application.
8.  [ ] Docker, CI/CD, logging, monitoring, and security hardening.
9.  [ ] System design fundamentals, caching, queues, and resilience.
10. [ ] Advanced database performance and distributed systems.
11. [ ] Cloud operations, infrastructure as code, and larger-scale
    architecture.
12. [ ] Revisit projects, improve architecture based on measured needs,
    and write design documents.

# Completion Review

Before calling yourself comfortable with full-stack development, try to
answer these questions without memorized scripts:

-   [ ] Can I trace a browser request from DNS lookup through HTTPS, the
    API, application logic, and database?
-   [ ] Can I design a relational schema and explain the constraints and
    indexes?
-   [ ] Can I build and test an API with validation, authentication,
    authorization, and consistent errors?
-   [ ] Can I build a responsive frontend that handles loading, empty,
    success, and failure states?
-   [ ] Can I debug an issue using logs, browser tools, a debugger, and
    database query plans?
-   [ ] Can I deploy the application and safely manage configuration,
    secrets, backups, and migrations?
-   [ ] Can I identify likely security vulnerabilities and test access
    controls?
-   [ ] Can I explain how the system behaves during a database outage,
    queue failure, or traffic spike?
-   [ ] Can I justify architecture choices based on requirements,
    measurements, and trade-offs?
-   [ ] Can another developer clone the project and run it using my
    documentation?

**Guiding principle:** Learn the simplest reliable solution first. Add
complexity---caching, queues, microservices, orchestration, and
multi-region deployment---when requirements or measurements justify it.
