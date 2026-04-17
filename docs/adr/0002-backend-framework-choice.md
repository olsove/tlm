# ADR 0002: Backend Framework Choice

## Status
Proposed

## Date
2026-04-18

## Context
The backend must support:
- domain-driven design with bounded contexts
- deterministic simulation orchestration and transactional consistency
- local-first deployment in Docker for v1
- a KISS approach for v1, while keeping a path to future event-driven evolution

The team has strong experience with Java and Spring, and wants to move quickly with low execution risk.

## Decision
Use Spring Boot 4.0 as the backend framework for v1, with:
- Java 21
- Spring Data JPA
- PostgreSQL
- Gradle Wrapper (Groovy DSL)

Architectural style:
- modular monolith
- internal (in-process) domain events
- no distributed message broker in v1

## Alternatives Considered
- Node.js + NestJS/Fastify: fast iteration and single-language stack with frontend, but weaker fit with current team experience and preferred backend architecture style.
- Quarkus: strong performance/startup profile, but less aligned with current team familiarity and existing Spring-oriented plans.
- Micronaut: lightweight and modern, but introduces extra learning and migration costs compared with Spring.

## Consequences
- Positive impact.
  - Higher delivery speed and confidence using known framework conventions.
  - Mature ecosystem for persistence, validation, transactions, and testing.
  - Strong alignment with DDD layering and future outbox/event-driven patterns.
- Negative impact.
  - More boilerplate than lighter frameworks in some areas.
  - Polyglot stack with React/TypeScript frontend and Java backend.
- Tradeoffs or follow-up work.
  - Define bounded context package/module boundaries early.
  - Define domain event catalogue and persistence strategy.
  - Reassess distributed event-driven architecture only when scaling signals justify it.

## Related
- [Architecture Suggestion](../ARCHITECTURE.md)
- [ADR 0001: Frontend Framework and Rendering Approach](./0001-frontend-framework-and-rendering-approach.md)
- [ADR Guide and Template](README.md)
