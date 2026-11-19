# 0003 — NestJS for the API

- Status: accepted
- Date: 2026-11-19

## Context

EN:
The API must host ten modules with strict boundaries (ADR 0001), real-time features, background jobs and good testability.

FR:
L'API doit intégrer dix modules dotés de limites strictes (ADR 0001), de fonctionnalités en temps réel, de tâches en arrière-plan et d'une bonne testabilité.

## Options considered

EN:

- NestJS 12: modules and dependency injection map directly to a modular monolith; built-in WebSocket gateways, queues and testing utilities; v12 adds Standard Schema (Zod) validation and an official observability SDK.
- Fastify: fast and light, but no imposed structure; the architecture of ten modules would be ours to invent and enforce.
- Hono: tiny and very well typed, designed for edge runtimes, which bring nothing on Kubernetes.

FR:

- NestJS 12 : les modules et l’injection de dépendances s’inscrivent directement dans une architecture monolithique modulaire ; passerelles WebSocket, files d’attente et utilitaires de test intégrés ; la v12 ajoute la validation via Standard Schema (Zod) et un SDK officiel d’observabilité.
- Fastify : rapide et léger, mais sans structure imposée ; il nous reviendrait d’inventer et de mettre en œuvre l’architecture composée de dix modules.
- Hono : minuscule et très bien typé, conçu pour les environnements d’exécution en périphérie, ce qui n’apporte rien sur Kubernetes.

## Decision

EN:
I use NestJS 12 with the Express HTTP adapter.

FR:
J'utilise NestJS 12 avec l'adaptateur HTTP Express.

## Consequences

EN:

- Easier: module boundaries, dependency injection, consistent patterns across modules.
- Harder: more boilerplate (decorators) and a learning curve.
- Express adapter because the Better Auth NestJS integration only supports Fastify in beta (ADR 0006). Switching to Fastify later requires measurements and a new ADR.

FR:

- Avantages : délimitation des modules, injection de dépendances, modèles cohérents d'un module à l'autre.
- Inconvénients : davantage de code standard (décorateurs) et une courbe d'apprentissage.
- Adaptateur Express, car l'intégration « Better Auth » dans NestJS ne prend en charge que Fastify en version bêta (ADR 0006). Le passage à Fastify ultérieurement nécessitera des tests de performance et un nouvel ADR.
