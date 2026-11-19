# 0002 — TypeScript end to end, in a pnpm + Turborepo monorepo

- Status: accepted
- Date: 2026-11-18

## Context

EN:
The API and the web app share data shapes (films, reviews, users).

FR:
L'API et l'application web partagent les mêmes structures de données (films, critiques, utilisateurs).

## Options considered

EN:

- TypeScript for both front and back: one language, shared types and validation schemas.
- Java/Kotlin (Spring Boot) back + TypeScript front: very robust, strong in large companies, but two languages and a steeper learning curve.
- Python (FastAPI) back: best AI ecosystem, but less structure for a large application.
- Separate repositories vs monorepo: a monorepo keeps shared code and atomic changes in one place.

FR:
FR:

- TypeScript pour le front-end et le back-end : un seul langage, des types et des schémas de validation partagés.
- Java/Kotlin (Spring Boot) pour le back-end + TypeScript pour le front-end : très robuste, très répandu dans les grandes entreprises, mais deux langages et une courbe d'apprentissage plus raide.
- Python (FastAPI) pour le back-end : le meilleur écosystème d’IA, mais moins structuré pour une application de grande envergure.
- Référentiels séparés ou monoréférentiel : un monoréférentiel permet de regrouper le code partagé et les modifications atomiques en un seul endroit.

## Decision

EN:
We use TypeScript for the API and the web app, in a single monorepo managed with pnpm workspaces and Turborepo. Python will be added in phase 3 for the AI service only.

FR:
J'utilise TypeScript pour l'API et l'application web, au sein d'un monorepo unique géré à l'aide de pnpm workspaces et de Turborepo. Python sera ajouté lors de la phase 3, uniquement pour le service d'IA.

## Consequences

EN:

- Easier: shared validation schemas in `packages/shared`, one toolchain, one CI pipeline.
- Harder: build caching and task ordering must be configured (Turborepo).
- To watch: all workspaces must use the same TypeScript major version.

FR:

- Avantages : schémas de validation partagés dans `packages/shared`, une seule chaîne d'outils, un seul pipeline d'intégration continue.
- Inconvénients : la mise en cache des builds et l'ordre des tâches doivent être configurés (Turborepo).
- À surveiller : tous les espaces de travail doivent utiliser la même version majeure de TypeScript.
