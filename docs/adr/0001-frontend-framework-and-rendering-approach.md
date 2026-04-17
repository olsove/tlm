# ADR 0001: Frontend Framework and Rendering Approach

## Status
Accepted

## Date
2026-04-18

## Context
The game is planned as a browser-based experience with a Spring backend, local Docker deployment for v1, and a strong focus on interactive systems:
- zone maps and state transitions
- command-driven simulation feedback
- progressive discovery of fragments and anomalies

The UI will be highly interactive and session-oriented, with frequent client-side updates after player commands. For v1, simplicity and fast iteration are prioritised (KISS), while preserving room for future scaling.

## Decision
Use:
- React + TypeScript as the frontend framework.
- Vite as the frontend build and development tool.
- Client-side rendering (CSR) as the rendering approach for v1.

Rendering model for v1:
- initial page shell loads in browser
- game state is fetched from backend APIs
- subsequent updates are command/response and state refresh cycles

No SSR/SSG is introduced in v1.

## Alternatives Considered
- React with SSR framework (for example Next.js): stronger out-of-the-box SEO and server rendering, but adds complexity not needed for an authenticated, interaction-heavy game client.
- Remix/React Router SSR-first approach: good data loading patterns, but additional operational and architectural overhead for v1.
- Static-only approach with minimal framework: simple delivery, but weak fit for complex interactive state and long-term UI evolution.

## Consequences
- Positive impact.
  - Fast development cycle and straightforward local Docker setup.
  - Excellent fit for highly interactive, simulation-driven UI behaviour.
  - Clear separation between frontend presentation and backend game/domain logic.
- Negative impact.
  - First paint depends on client bundle and API round-trip.
  - No SEO benefit from SSR in v1 (acceptable for current scope).
- Tradeoffs or follow-up work.
  - Optimise bundle size and route-level loading as the UI grows.
  - Reassess SSR/streaming if public, content-heavy pages become a core requirement.
  - Keep API contracts stable to support future frontend evolution.

## Related
- [Architecture Suggestion](../ARCHITECTURE.md)
- [ADR 0002: Backend Framework Choice](./0002-backend-framework-choice.md)
- [ADR Guide and Template](README.md)
