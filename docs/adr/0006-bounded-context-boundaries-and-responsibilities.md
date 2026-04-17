# ADR 0006: Bounded Context Boundaries and Responsibilities

## Status
Accepted

## Date
2026-04-18

## Context
The architecture adopts domain-driven design with a modular monolith in v1.
To avoid accidental coupling and unclear ownership, the system needs explicit bounded context boundaries and responsibility definitions.

The game includes shared simulation mechanics, variant-specific rules, lore discovery, and anomaly behaviour. These concerns evolve at different rates and should not be mixed in a single domain model.

## Decision
Define the following bounded contexts and responsibilities:

- **Session Context**
Owns game session lifecycle, tick progression, save/checkpoint ownership, and session-level invariants.

- **Structure Context**
Owns zones, links, energy routing rules, subsystem state transitions, and topology invariants.

- **Anomaly Context**
Owns instability calculations, anomaly emergence/escalation rules, and anomaly effects on available actions/state.

- **Lore Context**
Owns lore fragment catalogue, unlock criteria, and discovered-fragment consistency per session.

- **Variant Rules Context**
Owns variant policies and rule composition for `drift-protocol`, `entropy-rising`, and `broken-orbit`.

Integration rules:
- Contexts communicate through explicit application services and internal domain events.
- No context directly mutates another context’s internal aggregates.
- Cross-context reads use defined query interfaces/projections.

## Alternatives Considered
- Single unified domain model: simpler early structure, but high long-term coupling and unclear ownership.
- Per-variant full context duplication: stronger isolation, but duplicates shared concepts and increases maintenance overhead.
- Immediate microservice split by context: clean runtime isolation, but too much complexity for v1 and KISS goals.

## Consequences
- Positive impact.
  - Clear ownership and reduced cross-domain ambiguity.
  - Better maintainability as variant logic and shared systems evolve independently.
  - Easier path to future extraction into services if scaling requires it.
- Negative impact.
  - More up-front design effort and boundary discipline.
  - Some orchestration complexity in application layer for cross-context flows.
- Tradeoffs or follow-up work.
  - Define aggregate roots and invariants per context in implementation docs.
  - Define an initial domain event catalogue and publisher/subscriber responsibilities.
  - Add architecture tests/conventions to prevent boundary violations.

## Related
- [Architecture Suggestion](../ARCHITECTURE.md)
- [ADR 0002: Backend Framework Choice](./0002-backend-framework-choice.md)
- [ADR 0004: Simulation Model (Turn/Tick Deterministic Engine)](./0004-simulation-model-turn-tick-deterministic-engine.md)
- [ADR 0005: Monorepo Folder Layout for Three Variants](./0005-monorepo-folder-layout-for-three-variants.md)
- [ADR Guide and Template](README.md)
