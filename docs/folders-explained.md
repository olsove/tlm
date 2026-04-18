# Folder Structure Explained

This document explains the purpose of each top-level folder in the repository and the shared subfolders.

## Root Folders

- `drift-protocol/`
Holds variant-specific game content for **Drift Protocol**.  
Use this for mechanics, configuration, assets, and balancing that are unique to this variant.

- `entropy-rising/`
Holds variant-specific game content for **Entropy Rising**.  
Use this for decay/instability-focused gameplay rules and assets unique to this variant.

- `broken-orbit/`
Holds variant-specific game content for **Broken Orbit**.  
Use this for anomaly-navigation mechanics, content, and assets unique to this variant.

- `shared/`
Contains code and content reused across all variants.  
Only place items here when they are genuinely cross-variant.

- `backend/`
Contains the backend application (Spring Boot), including API endpoints, simulation orchestration, domain logic, persistence, and migrations.

- `frontend/`
Contains the browser client application (React + TypeScript), including UI, state management, routing, and variant-aware presentation logic.

- `docs/`
Contains architecture, ADRs, narrative/variant documentation, and other project documentation.

## Shared Subfolders

- `shared/engine/`
Shared deterministic simulation engine components and primitives used by multiple variants.

- `shared/lore/`
Shared lore/canon data, fragment catalogues, and cross-variant narrative dictionaries.

- `shared/ui-components/`
Reusable UI components/design primitives used by the frontend across variants.

## Placement Rules

- Put **shared canon** and **shared technical building blocks** in `shared/` or root docs.
- Put **variant-specific mechanics/content** in the matching variant folder.
- Avoid copying the same logic into multiple variant folders; promote to `shared/` when reuse is confirmed.
