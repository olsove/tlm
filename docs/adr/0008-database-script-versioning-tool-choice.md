# ADR 0008: Database Script Versioning Tool Choice

## Status
Accepted

## Date
2026-04-18

## Context
The project needs a reliable way to version and apply database schema changes across local development and containerised environments.

The chosen backend stack (Spring Boot + PostgreSQL) and deterministic simulation model will evolve schema over time (sessions, events, variant data, indexes). We need repeatable, traceable migrations in source control.

## Decision
Use Flyway for database script versioning and migration execution.

Adopt convention-based SQL migrations in the codebase (for example `V0001__...sql`) and apply migrations automatically at backend startup in local/dev environments.

Reason for this choice:
- the team is most familiar with Flyway
- low adoption risk and faster delivery
- straightforward integration with Spring Boot

## Alternatives Considered
- Liquibase: strong feature set (including XML/YAML/JSON changelogs), but higher complexity for current team preferences and workflow.
- Manual SQL scripts without a migration framework: low tooling overhead, but weak traceability, ordering guarantees, and environment consistency.
- ORM-driven schema generation only (`ddl-auto` style): fast for prototypes, but unsafe for controlled production-like evolution and rollback planning.

## Consequences
- Positive impact.
  - Predictable and auditable schema evolution.
  - Good fit for Docker-based local setup and CI workflows.
  - Lower onboarding and maintenance friction due to team familiarity.
- Negative impact.
  - Requires discipline in migration ordering and immutable migration history.
  - Complex data migrations may still require careful scripting and review.
- Tradeoffs or follow-up work.
  - Define migration naming/versioning standard for this repository.
  - Define policy for hotfix migrations and rollback strategy.
  - Add CI validation to ensure migrations apply on a clean database.

## Related
- [Architecture Suggestion](../ARCHITECTURE.md)
- [ADR 0003: Database and ORM Choice](./0003-database-and-orm-choice.md)
- [ADR 0002: Backend Framework Choice](./0002-backend-framework-choice.md)
- [ADR Guide and Template](README.md)
