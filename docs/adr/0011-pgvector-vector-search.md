# 0011 — pgvector for vector search

- Status: accepted
- Date: 2026-11-18

## Context

EN:
Phase 3 adds semantic search ("a film in London with an investigation") and search by image. Synopses, keywords and film images are turned into embeddings, and search means finding the nearest vectors, usually combined with filters (genre, year, not already watched).

FR:
La phase 3 ajoute la recherche sémantique (« un film à Londres avec une enquête ») et la recherche par image. Synopsis, mots-clés et images de films sont transformés en embeddings, et chercher revient à trouver les vecteurs les plus proches, en général combinés à des filtres (genre, année, pas encore vu).

## Options considered

EN:

- pgvector extension in PostgreSQL: vectors live next to relational data; filters and similarity in one SQL query; one system less to run.
- Dedicated vector database (Qdrant, Weaviate, Milvus): better at hundreds of millions of vectors and richer features, but another system to deploy and keep in sync.

FR:

- Extension pgvector dans PostgreSQL : les vecteurs vivent à côté des données relationnelles ; filtres et similarité dans une seule requête SQL ; un système de moins à exploiter.
- Base vectorielle dédiée (Qdrant, Weaviate, Milvus) : plus performante sur des centaines de millions de vecteurs et plus riche en fonctionnalités, mais un système de plus à déployer et à synchroniser.

## Decision

EN:
I use the pgvector extension in my PostgreSQL database.

FR:
J'utilise l'extension pgvector dans ma base PostgreSQL.

## Consequences

EN:

- Easier: one database, transactions, joins with user data (exclude watched films) in a single query.
- Harder: index tuning (HNSW) and memory sizing are on me.
- Each embedding stores its `model_version`, so a model change can be re-indexed without downtime.
- To watch: my expected volume is a few hundred thousand vectors. If it grows by orders of magnitude, revisit with a new ADR.

FR:

- Avantages : une seule base, des transactions, des jointures avec les données utilisateur (exclure les films vus) dans une seule requête.
- Inconvénients : le réglage des index (HNSW) et le dimensionnement mémoire sont à ma charge.
- Chaque embedding stocke sa `model_version`, ce qui permet de réindexer après un changement de modèle sans interruption.
- À surveiller : mon volume attendu est de quelques centaines de milliers de vecteurs. S'il augmente de plusieurs ordres de grandeur, réexaminer avec un nouvel ADR.
