# 0007 — TMDB as the film catalogue source

- Status: accepted
- Date: 2026-11-18

## Context

EN:
Judge needs films, people, companies, collections, release dates by country and posters. Building this catalogue myself is impossible; it must come from an external source.

FR:
Judge a besoin de films, de personnes, de sociétés, de sagas, de dates de sortie par pays et d'affiches. Construire ce catalogue moi-même est impossible : il doit venir d'une source externe.

## Options considered

EN:

- TMDB public API: broad coverage, French translations and release dates per country, free for non-commercial use with attribution.
- IMDb data: terms restrict use to personal and non-commercial purposes and forbid republishing.
- Several sources combined: better coverage, but much more matching and syncing work.

FR:

- API publique TMDB : large couverture, traductions françaises et dates de sortie par pays, gratuite pour un usage non commercial avec attribution.
- Données IMDb : les conditions limitent l'usage au cadre personnel et non commercial, et interdisent la republication.
- Plusieurs sources combinées : meilleure couverture, mais beaucoup plus de travail de rapprochement et de synchronisation.

## Decision

EN:
I use the TMDB public API, keep a local copy of the fields I need, and display TMDB attribution.

FR:
J'utilise l'API publique TMDB, je garde une copie locale des champs dont j'ai besoin, et j'affiche l'attribution TMDB.

## Consequences

EN:

- Easier: a rich catalogue from day one.
- Harder: I depend on TMDB quotas and availability; imports must be idempotent (`source` + `external_id` unique) and handle rate limits.
- Blocking before monetization: TMDB requires a commercial agreement for commercial use. A licence must be obtained before enabling the paywall.
- To watch: read TMDB's caching rules, since I keep a local copy.

FR:

- Avantages : un catalogue riche dès le premier jour.
- Inconvénients : je dépends des quotas et de la disponibilité de TMDB ; les imports doivent être idempotents (`source` + `external_id` uniques) et gérer la limitation de débit.
- Bloquant avant la monétisation : TMDB exige un accord commercial pour tout usage commercial. Une licence doit être obtenue avant d'activer le paywall.
- À surveiller : lire les règles de mise en cache de TMDB, puisque je garde une copie locale.
