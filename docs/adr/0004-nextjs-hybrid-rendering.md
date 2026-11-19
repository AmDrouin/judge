# 0004 — Next.js with hybrid rendering for the web app

- Status: accepted
- Date: 2026-11-19

## Context

EN:
Film pages and public profiles must be indexed by search engines and show a rich preview when shared (Open Graph). The rest of the app is highly interactive. The app must also be an installable PWA.

FR:
Les pages consacrées aux films et les profils publics doivent être référencés par les moteurs de recherche et afficher un aperçu détaillé lorsqu'ils sont partagés (Open Graph). Le reste de l'application est très interactif. L'application doit également être une PWA installable.

## Options considered

EN:

- Single Page Application: smooth, but crawlers and link previews see an empty page.
- Hybrid rendering (server-rendered public pages, interactive client app), with:
  - Next.js 16: largest React ecosystem, complete hybrid rendering, standalone output easy to containerize.
  - Nuxt 4 (Vue): clear conventions, smaller market.
  - SvelteKit: lightest, smaller component ecosystem and market.
  - TanStack Start: strongly typed, still young.

FR:

- Application monopage : fonctionnement fluide, mais les robots d'indexation et les aperçus de liens affichent une page vide.
- Rendu hybride (pages publiques rendues côté serveur, application client interactive), avec :
  - Next.js 16 : l'écosystème React le plus vaste, un rendu hybride complet, une sortie autonome facile à conteneuriser.
  - Nuxt 4 (Vue) : conventions claires, marché plus restreint.
  - SvelteKit : le plus léger, avec un écosystème de composants et un marché plus restreints.
  - TanStack Start : fortement typé, encore jeune.

## Decision

EN:
I use Next.js 16 with hybrid rendering.

FR:
J'utilise Next.js 16 avec le rendu hybride.

## Consequences

EN:

- Easier: SEO and share previews for public pages, large component ecosystem.
- Harder: App Router, Server Components and caching take time to master.
- Rule: Next.js renders pages and calls the NestJS API; it contains no business logic and never accesses the database directly.
- To watch: Next.js ships frequent security releases; Renovate must keep it patched.

FR:

- Avantages : référencement naturel (SEO) et aperçus de partage pour les pages publiques, vaste écosystème de composants.
- Inconvénients : l’App Router, les composants serveur et la mise en cache demandent du temps à maîtriser.
- Règle : Next.js effectue le rendu des pages et appelle l’API NestJS ; il ne contient aucune logique métier et n’accède jamais directement à la base de données.
- À surveiller : Next.js publie fréquemment des mises à jour de sécurité ; Renovate doit veiller à ce qu’il soit toujours à jour.
