# 0005 — PostgreSQL as primary database, Drizzle for schema and migrations

- Status: accepted
- Date: 2026-11-19

## Context

EN:
The data model is strongly relational (users, films, credits, follows, reviews). Migrations must run without downtime (expand/contract), and vector search must live close to the relational data (ADR 0011).

FR:
Le modèle de données est fortement relationnel (utilisateurs, films, crédits, abonnements, critiques). Les migrations doivent s'exécuter sans interruption de service (expand/contract), et la recherche vectorielle doit rester proche des données relationnelles (ADR 0011).

## Options considered

EN:

- Database: PostgreSQL is relational, mature, and supports vectors through the pgvector extension.
- Access layer:
  - Drizzle (0.45 stable, 1.0 in release candidate): schema in TypeScript, SQL-like queries, migrations generated as SQL files I review; vector column type.
  - Prisma (7 stable, 8 in release candidate): polished tooling, but abstracts SQL away and supports pgvector only through raw SQL.
  - Kysely with hand-written SQL: full control, more code to maintain.

FR:

- Base de données : PostgreSQL est relationnel, mature, et gère les vecteurs grâce à l'extension pgvector.
- Couche d'accès :
  - Drizzle (0.45 stable, 1.0 en release candidate) : schéma en TypeScript, requêtes proches du SQL, migrations générées sous forme de fichiers SQL que je relis ; type de colonne vectoriel.
  - Prisma (7 stable, 8 en release candidate) : outillage très abouti, mais masque le SQL et ne gère pgvector qu'en SQL brut.
  - Kysely avec du SQL écrit à la main : contrôle total, plus de code à maintenir.

## Decision

EN:
I use PostgreSQL with the pgvector extension, and Drizzle, pinned to `0.45.x`, for schema and migrations.

FR:
J'utilise PostgreSQL avec l'extension pgvector, et Drizzle, épinglé en `0.45.x`, pour le schéma et les migrations.

## Consequences

EN:

- Easier: every migration is a SQL file reviewed before commit; queries stay close to SQL.
- Harder: Drizzle 1.0 will change the relational query API; the upgrade needs planning.
- Rules: `strict` mode enabled for renames; never `push` the schema in production; no rollback tooling, so expand/contract is mandatory.
- To watch: the Drizzle team joined PlanetScale in March 2026; the project remains open source.

FR:

- Avantages : chaque migration est un fichier SQL relu avant le commit ; les requêtes restent proches du SQL.
- Inconvénients : Drizzle 1.0 modifiera l'API des requêtes relationnelles ; la mise à jour devra être planifiée.
- Règles : mode `strict` activé pour les renommages ; jamais de `push` du schéma en production ; aucun outil de retour arrière, donc l'expand/contract est obligatoire.
- À surveiller : l'équipe Drizzle a rejoint PlanetScale en mars 2026 ; le projet reste open source.
