# ADR 0004: Simulation Model (Turn/Tick Deterministic Engine)

## Status
Accepted

## Date
2026-04-18

## Context
The game requires a simulation model that supports:
- consistent state progression after player actions
- reliable debugging and reproducibility of outcomes
- clear integration with domain events and event logs
- variant-specific behaviour while preserving a shared core
- simple implementation for v1 (KISS) with room for future scaling

The narrative also depends on systemic behaviour and partial revelation, which benefits from predictable internal state transitions and controlled visibility.

## Decision
Adopt a deterministic turn/tick simulation engine for v1:
- player submits a command
- command is validated against current state
- engine executes a deterministic turn resolution
- tick advances and resulting state is persisted
- domain events and player-visible events are recorded

Model characteristics:
- server-authoritative simulation
- deterministic rules per variant (`drift-protocol`, `entropy-rising`, `broken-orbit`)
- explicit separation between full internal state and player-visible projection

## Alternatives Considered
- Real-time continuous simulation loop: more dynamic feel, but higher complexity for synchronisation, persistence, and debugging in v1.
- Non-deterministic/random-first simulation: can create surprise, but harder to reproduce issues and validate balancing.
- Fully event-sourced from day one: strong auditability, but high implementation overhead for v1 versus incremental event logging.

## Consequences
- Positive impact.
  - Predictable behaviour and easier balancing/testing.
  - Strong support for replay/debug workflows via command + tick + event history.
  - Clear fit with DDD boundaries and internal domain event publication.
- Negative impact.
  - Less “always alive” feel compared with full real-time simulation unless carefully presented in UX.
  - Requires discipline to keep rule logic deterministic across variants.
- Tradeoffs or follow-up work.
  - Define deterministic seed strategy for anomaly generation.
  - Add regression tests for tick resolution invariants.
  - Reassess partial real-time overlays later (for example ambient visual updates) without changing core deterministic engine.

## Related
- [Architecture Suggestion](../ARCHITECTURE.md)
- [ADR 0002: Backend Framework Choice](./0002-backend-framework-choice.md)
- [ADR 0003: Database and ORM Choice](./0003-database-and-orm-choice.md)
- [ADR Guide and Template](README.md)
