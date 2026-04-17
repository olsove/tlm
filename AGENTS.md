# AGENTS.md

## Purpose
This file defines contribution rules for coding agents working in this repository.
All changes must stay faithful to the narrative established in [README.md](README.md).

## Story Canon (Do Not Contradict)
- The origin of the Megastructure is unknown.
- The player is a custodian, not a conqueror.
- Knowledge is always partial; truth is inferred through fragments and behaviour.
- The Megastructure is ancient, vast, unstable, and still partially active.
- Mystery, ambiguity, and tension are core to tone and design.

## Root Structure
The repository is intended to contain three top-level game variants:
- `drift-protocol/`
- `entropy-rising/`
- `broken-orbit/`

When implementing or documenting features:
- Keep shared lore and cross-variant canon in root folder.
- Keep variant-specific mechanics and assets inside the matching variant folder.
- Avoid leaking one variant's unique mechanics into another unless explicitly marked as a shared canon.

## Variant Identity Rules
- **Drift Protocol**: hidden logic, protocol discovery, system-learning.
- **Entropy Rising**: decay pressure, instability management, survival trade-offs.
- **Broken Orbit**: anomaly navigation, spatial unreliability, surreal exploration.

## Writing and Language
- Use British English in all markdown and in-game text.
- Prefer: `behaviour`, `civilisation`, `optimise`, `analyse`, `colour`.
- Keep terms consistent across files (do not mix UK and US spellings).

## Documentation Expectations
- Update `README.md` when core narrative or shared assumptions change.
- Keep variant docs aligned with their key question and tone.
- Record all architectural decisions as ADRs in `docs/adr/`.
- Ensure each ADR clearly demonstrates that an informed decision has been made.
- For any new ADR, follow the rules and template in `docs/adr/README.md`.
- Set `Status` to `Proposed` for every newly created ADR.
- If an architectural decision is made in discussion or implementation, remind the user to create a corresponding ADR.

## Agent Workflow
1. Read `README.md` before making narrative, mechanics, or tone changes.
2. Identify whether the change is shared-canon or variant-specific.
3. Apply minimal, coherent edits in the correct folder/doc.
4. Verify spelling and terminology consistency across affected markdown files.
