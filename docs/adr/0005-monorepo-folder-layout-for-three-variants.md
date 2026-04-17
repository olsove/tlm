# ADR 0005: Monorepo Folder Layout for Three Variants

## Status
Accepted

## Date
2026-04-18

## Context
The project will contain three game variants:
- Drift Protocol
- Entropy Rising
- Broken Orbit

The repository must support:
- shared story canon and shared technical foundations
- clear separation of variant-specific mechanics and assets
- local-first development with Docker
- maintainable growth without early over-fragmentation

The game architecture follows a modular-monolith approach for v1 with shared simulation concepts and variant rules.

## Decision
Adopt a monorepo layout with explicit root folders per variant and a shared area for cross-variant code:

```text
/
  drift-protocol/
  entropy-rising/
  broken-orbit/
  shared/
    engine/
    lore/
    ui-components/
  backend/
  frontend/
  docs/
    adr/
```

Layout rules:
- Shared lore/canon and reusable technical modules go in `shared/` (or root docs for canonical narrative).
- Variant-specific mechanics, balancing data, and assets stay in their variant folder.
- Backend and frontend applications remain unified in v1 and load variant modules/configuration by variant id.

## Alternatives Considered
- Single app folder with all variants mixed inside feature modules: simpler initially, but higher risk of accidental coupling and weaker variant boundaries.
- Separate repositories per variant: stronger isolation, but duplicates shared logic and increases coordination overhead.
- Fully split deployable services/apps per variant in v1: flexible long-term, but excessive complexity for KISS-first delivery.

## Consequences
- Positive impact.
  - Clear ownership boundaries between shared and variant-specific content.
  - Easier onboarding and navigation for contributors.
  - Keeps path open for future extraction if one variant needs independent deployment.
- Negative impact.
  - Requires discipline to prevent `shared/` from becoming a dumping ground.
  - Some duplication may still occur where variant divergence is intentional.
- Tradeoffs or follow-up work.
  - Define contribution guardrails for what qualifies as shared vs variant-specific.
  - Add CI checks/linting conventions for folder boundaries where practical.
  - Reassess extraction strategy only when scale or team structure justifies it.

## Related
- [Architecture Suggestion](../ARCHITECTURE.md)
- [ADR 0002: Backend Framework Choice](./0002-backend-framework-choice.md)
- [ADR 0004: Simulation Model (Turn/Tick Deterministic Engine)](./0004-simulation-model-turn-tick-deterministic-engine.md)
- [ADR Guide and Template](README.md)
