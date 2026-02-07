<!--
Sync Impact Report:
===================
Version Change: INITIAL → 1.0.0
Rationale: Initial constitution creation for Todo Full-Stack Web Application

Added Sections:
- Core Principles (6 principles)
- Technology Stack
- Development Workflow
- Governance

Modified Principles: N/A (initial creation)
Removed Sections: N/A (initial creation)

Templates Status:
✅ .specify/templates/spec-template.md - Aligned (spec-first requirement matches)
✅ .specify/templates/plan-template.md - Aligned (constitution check section exists)
✅ .specify/templates/tasks-template.md - Aligned (task structure supports workflow)

Follow-up TODOs:
- None (all placeholders filled)

Date: 2026-01-09
-->

# Todo Full-Stack Web Application Constitution

## Core Principles

### I. Spec-First Development (NON-NEGOTIABLE)

Every feature MUST originate from an explicit, approved specification before any implementation work begins. This principle ensures all development is intentional, traceable, and reviewable.

**Rules**:
- No implementation code may be written without a corresponding approved spec
- Specs MUST be completed and approved before planning begins
- Plans MUST be derived strictly from specs with no additional scope
- Tasks MUST map one-to-one with plan items
- All REST API endpoints MUST be defined in specs before implementation

**Rationale**: Spec-first development creates an auditable trail from requirements to implementation, enabling hackathon reviewers to trace every feature decision and ensuring reproducibility of results.

### II. Agentic Dev Stack Compliance (NON-NEGOTIABLE)

All development MUST follow the strict workflow: spec → plan → tasks → execution. This workflow ensures proper decomposition, planning, and systematic execution.

**Rules**:
- Workflow phases MUST execute in order: spec → plan → tasks → execution
- Each phase MUST complete and be approved before the next begins
- No phase skipping or workflow shortcuts permitted
- All code MUST be generated via Claude Code agents (zero manual coding)
- Each phase output MUST be documented and version-controlled

**Rationale**: The agentic workflow ensures systematic development, proper planning, and enables multiple reviewers or agents to reproduce the exact development process.

### III. Security by Design (NON-NEGOTIABLE)

Security MUST be enforced at every layer with authentication, authorization, and data isolation as foundational requirements, not afterthoughts.

**Rules**:
- All REST API endpoints MUST require valid JWT authentication
- Requests without valid JWT MUST return 401 Unauthorized
- User ID in JWT MUST match user ID in API request path for user-scoped operations
- Each user can ONLY view or modify their own tasks (data isolation)
- Backend MUST independently verify JWTs without relying on frontend sessions
- Shared secrets MUST be environment-based and never hardcoded
- Authentication MUST be stateless using JWT

**Rationale**: Security violations and cross-user data leakage would be critical failures in a multi-user todo application. Enforcing security by design prevents these issues from the start.

### IV. Clear Separation of Concerns

The architecture MUST maintain distinct boundaries between frontend, backend, database, and authentication layers with no cross-contamination of responsibilities.

**Rules**:
- Frontend and backend MAY communicate ONLY via documented REST APIs
- No direct database access from frontend
- Authentication logic isolated in dedicated auth service/module
- Each layer has a single, well-defined responsibility
- Data models are defined once and shared via documented contracts
- API contracts MUST be documented before implementation

**Rationale**: Clear separation enables independent development, testing, and modification of each layer without cascading changes or hidden dependencies.

### V. Reproducibility and Traceability

Every development decision and implementation MUST be traceable from specs through execution, enabling external reviewers to reproduce results using only specs and documented prompts.

**Rules**:
- All REST API behavior MUST exactly match written specs
- Architectural decisions MUST be documented with rationale and tradeoffs
- Prompt History Records (PHRs) MUST be created for all significant development sessions
- Architecture Decision Records (ADRs) MUST document significant technical choices
- All implementation steps MUST be auditable through version control
- Reviewers MUST be able to reproduce results using documented specs and prompts

**Rationale**: Hackathon judges and future maintainers need to understand why decisions were made and verify that implementation matches specifications exactly.

### VI. Technology Stack Fixation

The technology stack MUST remain fixed throughout the project to ensure consistency, compatibility, and successful integration.

**Rules**:
- Frontend: Next.js 16+ (React Server Components, App Router)
- Backend: FastAPI (Python)
- ORM: SQLModel
- Database: Neon Serverless PostgreSQL
- Authentication: Better Auth with JWT
- NO technology substitutions permitted without constitutional amendment
- All dependencies MUST be compatible with the fixed stack

**Rationale**: Mixed or inconsistent technologies lead to integration issues, security vulnerabilities, and maintenance complexity. A fixed stack ensures all components work together seamlessly.

## Technology Stack

### Mandated Technologies

**Frontend Stack**:
- Framework: Next.js 16+ with App Router
- Component Model: React Server Components + Client Components
- Styling: Tailwind CSS
- Type Safety: TypeScript

**Backend Stack**:
- Framework: FastAPI (Python 3.11+)
- ORM: SQLModel (combines SQLAlchemy + Pydantic)
- Database: Neon Serverless PostgreSQL
- Authentication: Better Auth with JWT (RS256)
- API Documentation: OpenAPI/Swagger (auto-generated by FastAPI)

**Development Tools**:
- Code Generation: Claude Code (all code must be AI-generated)
- Version Control: Git
- Documentation: Markdown (specs, plans, tasks, ADRs, PHRs)

### Integration Requirements

- Frontend communicates with backend ONLY via REST APIs
- Backend connects to Neon PostgreSQL via connection string
- JWT tokens signed with RS256 algorithm
- Environment variables for all secrets and configuration
- CORS properly configured for frontend-backend communication

## Development Workflow

### Phase Gate Requirements

**Gate 1: Spec Approval**
- All functional requirements documented
- API contracts fully specified
- Success criteria defined and measurable
- Edge cases identified
- User stories with acceptance scenarios complete

**Gate 2: Plan Approval**
- Architecture designed per spec requirements
- Component responsibilities clearly defined
- API endpoint contracts documented
- Database schema designed
- Technology choices justified

**Gate 3: Task Approval**
- All tasks map to plan items
- Dependencies clearly identified
- Acceptance criteria for each task
- Estimated complexity documented
- Parallel execution opportunities identified

**Gate 4: Implementation Complete**
- All tasks executed via Claude Code
- API behavior matches specs exactly
- Authentication and authorization enforced
- User data properly isolated
- All HTTP status codes correct

### Code Generation Requirements

- ALL code MUST be generated by Claude Code agents
- NO manual coding permitted at any stage
- REST API endpoints MUST follow defined URL structure and HTTP methods
- After authentication enabled, all endpoints MUST require valid JWT
- Backend MUST independently verify JWTs

### Documentation Requirements

- **Prompt History Records (PHRs)**: Created for all significant development sessions
- **Architecture Decision Records (ADRs)**: Created for all architecturally significant decisions
- **API Documentation**: All endpoints documented with request/response schemas
- **Setup Documentation**: Project MUST be runnable using documented setup steps

## Governance

### Amendment Procedure

1. Proposed amendment documented with rationale and impact analysis
2. All affected templates and documents identified
3. Version number incremented per semantic versioning:
   - **MAJOR**: Backward-incompatible changes, principle removals, or redefinitions
   - **MINOR**: New principles added or material expansions
   - **PATCH**: Clarifications, wording fixes, non-semantic refinements
4. All dependent artifacts updated for consistency
5. Amendment approved and constitution updated
6. Changes propagated to all affected documents

### Compliance and Review

- All development work MUST verify compliance with this constitution
- Spec, plan, and task reviews MUST check constitutional alignment
- Any complexity or constraint violations MUST be explicitly justified
- Constitution supersedes all other practices and guidelines
- Reviewers MUST be able to trace features from spec to implementation

### Success Criteria

The project is considered successful when:
- All three specs (Backend, Frontend, Authentication) are fully implemented and integrated
- All five basic Todo features work correctly in a multi-user environment
- Users can sign up, sign in, and manage only their own tasks
- Persistent storage is verified using Neon Serverless PostgreSQL
- Secure JWT-based authentication is enforced across all APIs
- Unauthorized access and cross-user data leakage are impossible
- API responses use correct HTTP status codes
- The full spec → plan → task → execution workflow is auditable
- Hackathon reviewers can trace every feature from spec to implementation

**Version**: 1.0.0 | **Ratified**: 2026-01-09 | **Last Amended**: 2026-01-09
