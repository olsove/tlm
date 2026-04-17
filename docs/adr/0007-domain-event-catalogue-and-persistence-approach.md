# ADR 0007: Domain Event Catalogue and Persistence Approach

## Status
Accepted

## Date
2026-04-18

## Context
The architecture uses DDD with bounded contexts and a deterministic turn/tick simulation model.
The system needs a clear event catalogue and persistence strategy to support:
- traceability of game state changes
- debugging and replay of simulation behaviour
- decoupling between bounded contexts through internal events
- a future migration path to event-driven integration if scaling requires it

For v1, KISS applies: modular monolith, no distributed broker, and low operational complexity.

## Decision
Adopt an internal domain event model with a versioned event catalogue and persisted event records.

Event catalogue (initial):
- `SessionStarted`
- `CommandAccepted`
- `TickAdvanced`
- `EnergyRerouted`
- `ZoneStabilised`
- `AnomalyDetected`
- `AnomalyEscalated`
- `FragmentRecovered`

Event persistence approach:
- persist domain events in a dedicated `domain_event` table
- include fields: `id`, `session_id`, `tick`, `context`, `event_name`, `event_version`, `payload(jsonb)`, `occurred_at`
- append-only writes; no updates to historical events
- keep player-facing `event_log` projection separate from internal domain events

Publication approach (v1):
- publish/consume domain events in-process inside the modular monolith
- use application services/handlers for cross-context reactions
- no external message broker in v1

## Alternatives Considered
- No formal catalogue, ad hoc event naming: fastest start, but weak consistency and higher long-term maintenance risk.
- Full event sourcing from day one: strong auditability, but too much complexity for v1 delivery goals.
- Immediate external broker integration (Kafka/RabbitMQ): useful for distributed scale, but unnecessary operational overhead in v1.

## Consequences
- Positive impact.
  - Consistent language and contracts across contexts.
  - Improved observability, auditing, and replay/debug capabilities.
  - Clear upgrade path to outbox + broker patterns later.
- Negative impact.
  - Requires governance of event versions and payload schemas.
  - Additional storage overhead for persisted events.
- Tradeoffs or follow-up work.
  - Define event schema/versioning conventions and compatibility rules.
  - Add retention/archival policy for high-volume event tables.
  - Introduce outbox pattern only when asynchronous external integration is required.

## Related
- [Architecture Suggestion](../ARCHITECTURE.md)
- [ADR 0004: Simulation Model (Turn/Tick Deterministic Engine)](./0004-simulation-model-turn-tick-deterministic-engine.md)
- [ADR 0006: Bounded Context Boundaries and Responsibilities](./0006-bounded-context-boundaries-and-responsibilities.md)
- [ADR Guide and Template](README.md)
