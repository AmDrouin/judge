# 0008 — Pull-based activity feed for the MVP

- Status: accepted
- Date: 2026-11-18

## Context

EN:
The Home screen shows recent activity (reviews, likes, lists) from the people and entities a user follows. I must choose when this feed is computed.

FR:
L'écran Accueil affiche l'activité récente (critiques, j'aime, listes) des personnes et des entités qu'un utilisateur suit. Je dois choisir à quel moment ce fil est calculé.

## Options considered

EN:

- Pull (fan-out on read): the feed is queried when the user opens Home. Simple, no extra storage; cost grows with the number of followed accounts.
- Push (fan-out on write): each new activity is copied into every follower's feed. Instant reads, but an account with many followers triggers many writes.
- Hybrid: push for regular accounts, pull for very popular ones.

FR:

- Pull (calcul à la lecture) : le fil est requêté quand l'utilisateur ouvre l'Accueil. Simple, sans stockage supplémentaire ; le coût augmente avec le nombre de comptes suivis.
- Push (calcul à l'écriture) : chaque nouvelle activité est copiée dans le fil de chaque abonné. Lecture instantanée, mais un compte avec beaucoup d'abonnés déclenche beaucoup d'écritures.
- Hybride : push pour les comptes ordinaires, pull pour les comptes très suivis.

## Decision

EN:
I start with a pull-based feed built from the `activity` table, and move to a hybrid model when a measurement justifies it.

FR:
Je commence par un fil en pull construit à partir de la table `activity`, et je passerai à un modèle hybride quand une mesure le justifiera.

## Consequences

EN:

- Easier: no `feed_item` table, no fan-out workers in the MVP.
- Harder: the feed query must be well indexed (`actor_id`, `created_at`) and paginated by cursor.
- To watch: feed query latency (p95). Crossing the agreed threshold triggers the switch to hybrid and a new ADR.

FR:

- Avantages : pas de table `feed_item`, pas de workers de diffusion dans le MVP.
- Inconvénients : la requête du fil doit être bien indexée (`actor_id`, `created_at`) et paginée par curseur.
- À surveiller : la latence de la requête du fil (p95). Le dépassement du seuil fixé déclenche le passage à l'hybride et un nouvel ADR.
