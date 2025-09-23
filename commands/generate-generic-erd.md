---
name: Generate Engineering Design Doc (Generic Feature)
description: Create a senior-level engineering design document for any software feature (web, mobile, backend, desktop), optimized for AI agent implementation with clear contracts, performance/scalability, maintainability, and exhaustive testability.
parameters:
  - name: feature_name
    type: string
    required: true
    description: Short, human-readable feature name (e.g., "Offline Sync")
  - name: feature_description
    type: string
    required: false
    description: Brief problem, value, and success criteria for the feature
  - name: architecture_preference
    type: string
    required: false
    description: Preferred architecture/patterns (e.g., Clean Architecture, MVC/MVVM, Redux, CQRS) or "decide"
  - name: tech_stack
    type: string
    required: false
    description: Preferred technologies/frameworks/languages (e.g., React, Kotlin, Go, Postgres) or "decide"
  - name: constraints
    type: string
    required: false
    description: Legal, privacy, platform, performance, or device constraints
  - name: risks
    type: string
    required: false
    description: Top risks and mitigations
  - name: performance_targets
    type: string
    required: false
    description: Budget targets (e.g., p95 latency, throughput, memory, cold start)
  - name: testing_notes
    type: string
    required: false
    description: Any specific testing requirements or areas of focus
  - name: references
    type: string
    required: false
    description: Useful links (docs, blog posts, comps) to inform the design
---

You are a senior software engineer. Generate a detailed, implementation-ready engineering design document in Markdown for a software feature that may target web, mobile, backend services, desktop, or multi-tier systems. Optimize for clarity, simplicity, long-term maintainability, and AI agent consumption. Write the file to the top level of this repository unless instructed otherwise with a kebab-cased filename derived from the feature name (e.g. offline-sync-design.md). Be explicit about interfaces, inputs/outputs, error cases, and contracts. Favor concise bullets, clear headings, and scannable tables. Use only '##' and '###' headings.

If there is a selection present, treat it as additional notes. Inputs:
- Feature Name: {{feature_name}}
- Feature Description: {{feature_description}}
- Architecture Preference: {{architecture_preference}}
- Tech Stack: {{tech_stack}}
- Constraints: {{constraints}}
- Risks: {{risks}}
- Performance Targets: {{performance_targets}}
- Testing Notes: {{testing_notes}}
- References: {{references}}

Also incorporate relevant ideas from the current selection if provided:
{{selection}}

Generate the design using the structure below.

## Engineering Design Document

### Overview
- **Feature**: {{feature_name}}
- **Summary**: What this does and why it matters in one or two sentences.
- **Problem**: The user and system problems this solves.
- **Scope**: In-scope and out-of-scope.
- **Platforms/Environments**: e.g., Web, iOS, Android, Backend service (Linux), Desktop, Cloud provider/region.
- **Assumptions**: Call out any assumptions that, if wrong, change the design.
- **Domain Context**: Briefly describe domain model and key entities (if applicable).
- **References**: {{references}}

### Goals and Non-Goals
- **Goals**: Intended outcomes and user value.
- **Non-Goals**: Explicitly excluded to prevent scope creep.
- **Success Metrics**: Observable, quantifiable indicators (adoption, p95 latency, throughput, error rate, crash-free sessions).

### Architecture and Design
- **Pattern & Rationale**: Clean architecture with clear separation of concerns (Presentation/UI, State/Controllers, Domain/Use-Cases, Data/Integration). Prefer SRP for classes and avoid bloated files; extract modules/components/services when files approach 500–600 lines.
- **Architecture Preference**: Use {{architecture_preference}} and/or {{tech_stack}} if provided; otherwise pick an appropriate modern approach based on complexity, testability, and team expertise.
- **System Boundaries**:
  - Client(s) ↔ Server(s) ↔ Data Stores ↔ External Services
  - Call out trust boundaries and synchronous vs. asynchronous interactions.
- **Data Flow (Unidirectional where possible)**:
  - UI/Clients → Intents/Requests → Business Logic/State → Effects/Responses → Rendered UI/Outputs
  - Include how errors and loading states propagate.
- **Module Decomposition**:
  - Presentation (screens/pages/views/components)
  - State/Controllers (notifiers, blocs, view models, controllers)
  - Domain (use-cases/interactors)
  - Data (repositories, data sources, gateways)
  - Integration (HTTP/gRPC/GraphQL, message queues, schedulers)
  - Note boundaries and dependencies to minimize coupling.

### Component Interfaces (AI-Ready Contracts)
Provide deterministic, copy-pastable contracts for each component. Include inputs, outputs, errors, and side-effects. Prefer immutability for models.

- **Screens/Pages/Views or UI Components**
  - Purpose, key props/state, navigation/entry params, accessibility and theming (light/dark/high contrast).
- **State Objects (Controller/BLoC/Notifier/ViewModel)**
  - Inputs (events/actions), outputs (states), side-effects, error mapping.
- **Use Cases / Services**
  - Function signature, inputs, outputs, error types, idempotency.
- **Repositories / Data Access**
  - Methods, request/response models, caching policy, offline behavior, retry/backoff.
- **APIs (Internal/External)**
  - Endpoints (HTTP/gRPC/GraphQL), payload schemas, timeouts, auth, error codes.
- **Storage**
  - Local/remote DB/tables, indexes/keys, migration strategy, retention, export/import implications.
- **Background Jobs / Schedulers / Queues**
  - Triggers, schedules/CRON, inputs/outputs, retry/backoff, DLQ handling.

Where helpful, include short tables like:

| Component | Input | Output | Errors | Notes |
|---|---|---|---|---|
| OrderRepository.getByDateRange | dateRange | List<Order> | NetworkError, ParseError | Cached 15 min |

### API and Data Handling
- **Endpoints/Interfaces**: List method, path/topic, request/response shapes, auth, pagination/streaming, versioning.
- **Validation**: Client- and server-side validation rules and error messages.
- **Serialization**: Immutable models; JSON/Proto/Avro schemas; nullability; versioning plan.
- **Caching**: In-memory, CDN, and disk caches; eviction strategy; staleness policy.
- **Offline/Degraded Modes**: Queuing, conflict resolution (last-write-wins, merge, CRDTs), reconciliation.
- **Error Handling**: Error taxonomy → UI states or API responses; user messages vs. logs; retryability.

### Database Schema (Approval Gate)
- Proposed schema changes with tables/collections, columns/fields, types, indexes, and relationships.
- Migration plan and rollback.
- Data retention and PII handling.
- Import/Export impact and updates required.
STOP: Present schema here for approval before implementation.

### Performance and Scalability Plan
- **Targets**: {{performance_targets}} (e.g., p95 latency < X ms, throughput Y rps, memory < Z MB, cold start < T s).
- **Rendering/Processing**: Avoid unnecessary re-renders/work; memoize; virtualization/streaming where appropriate; batch and debounce.
- **Data Volumes**: Expected growth rates; pagination; batching; streaming; hot vs. cold paths.
- **Scalability**: Horizontal/vertical scaling strategies; partitioning/sharding; backpressure.
- **Background Work**: Scheduling, throttling, retries, backoff, battery/network constraints (for mobile), cost controls.
- **Profiling Plan**: How to measure (APM, DevTools, tracing, flame charts), and what to fix if targets miss.

### Security, Privacy, and Compliance
- AuthN/AuthZ, secure storage, transport security (TLS), key management.
- PII minimization, encryption at rest and in transit, data deletion/export pathways.
- Threat model, input sanitization, injection and XSS/CSRF/SSRF protections, rate limiting.
- Permissions and platform-specific prompts/copies (e.g., camera/photos/notifications on mobile; scopes on web/desktop).
- Compliance considerations (e.g., GDPR/CCPA/HIPAA/FERPA) as applicable.

### UX, Accessibility, and Theming
- Adaptive/responsive layouts; device rotation and window resizing support.
- Light and dark themes; high contrast; text scaling; semantic labels; keyboard navigation; large tap targets.
- Navigation/back handling patterns; avoid deprecated APIs; consistent routing and deep-linking if applicable.

### Logging, Telemetry, and Observability
- Use a structured logger (avoid print). Include event names, context, correlation/trace IDs, and error details.
- Metrics to emit (SLIs/SLOs); dashboards/alerts to build; breadcrumbing for repro.
- Audit logs for sensitive operations.

### Testing Strategy
- **Unit Tests**: High coverage for services, repositories, state, and use-cases. Mock external systems with suitable libraries.
- **Component/Widget/Integration Tests**: Deterministic rendering and interactions; golden/snapshot tests for key states where relevant.
- **End-to-End Tests**: At least one real path with actual DB/network if applicable; otherwise use test servers/sandboxes.
- **Test Cases (Given/When/Then)**:
  - Given [precondition]
  - When [action]
  - Then [assertions]
- **CI**: Static analysis/lint, format, unit/component/e2e suites, coverage thresholds, security checks.

### Risks and Mitigations
{{risks}}

### Constraints and Dependencies
{{constraints}}

### Rollout and Maintenance
- Feature flags/kill switches; staged rollout and canary.
- Migration/backward compatibility.
- Runbooks, on-call handoff notes, SLOs and error budgets.
- Ownership and code locations.

### Open Questions
- Decisions needed and owners.

### Change Log
- Track notable decisions and revisions to this design.

---

References and notes for implementers:
- Twelve-Factor App: https://12factor.net
- Architectural Patterns (overview): https://martinfowler.com/architecture
- Microservices Patterns (overview): https://microservices.io/patterns/index.html
- OWASP Cheat Sheet Series: https://owasp.org/www-project-cheat-sheet-series/
- Accessibility Guidance (WAI): https://www.w3.org/WAI/standards-guidelines/
- Testing Pyramid/Trophy discussion: https://martinfowler.com/bliki/TestPyramid.html , https://kentcdodds.com/blog/the-testing-trophy-and-testing-classifications

