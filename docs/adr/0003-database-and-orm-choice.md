# ADR 0003: Database and ORM Choice

## Status
Accepted

## Date
2026-04-18

## Context
The backend requires a persistence approach that supports:
- transactional consistency for command processing and simulation ticks
- structured relational data (sessions, zones, links, unlocks)
- flexible payload storage for logs/events/metadata
- local-first Docker deployment for v1
- future evolution to domain events and possible outbox integration

The chosen backend stack is Spring Boot with Spring Data, and the architecture is a modular monolith following KISS for v1.

## Decision
Use:
- Database: PostgreSQL
- ORM/persistence approach: Spring Data JPA (Hibernate as provider)

Data modelling approach:
- relational schema for core domain entities and invariants
- JSONB columns where event payloads or metadata benefit from flexible structure
- explicit migrations managed in source control

## Alternatives Considered
- MySQL + Spring Data JPA: solid relational option, but PostgreSQL offers stronger JSON/JSONB ergonomics and querying flexibility for event-oriented payloads.
- MongoDB + Spring Data MongoDB: flexible documents, but weaker fit for strict relational invariants and transactional modelling across core game entities.
- Plain JDBC/jOOQ-only approach: high SQL control, but increased development overhead for v1 compared with JPA conventions and repository support.

## Consequences
- Positive impact.
  - Strong transactional model for deterministic simulation updates.
  - Mature Spring integration and broad ecosystem support.
  - Good balance of relational integrity and flexible event/metadata storage.
- Negative impact.
  - ORM abstraction can hide inefficient queries if not monitored.
  - Mapping complexity can increase as domain models evolve.
- Tradeoffs or follow-up work.
  - Define indexing strategy for session and event queries early.
  - Add query performance checks for hot paths.
  - Revisit selective use of native SQL/jOOQ for complex reporting queries if needed.

## Related
- [Architecture Suggestion](../ARCHITECTURE.md)
- [ADR 0002: Backend Framework Choice](./0002-backend-framework-choice.md)
- [ADR Guide and Template](README.md)
