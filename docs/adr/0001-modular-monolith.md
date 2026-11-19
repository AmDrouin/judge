# 0001 — Modular monolith with a separate real-time gateway

- Status: accepted
- Date: 2026-11-18

## Context

EN:
Judge covers several products in one: a film journal, discussions, real-time messaging, events and AI recommendations. I build it solo and it must run in production at a reasonable cost, while staying easy to reason about.

FR:
Judge regroupe plusieurs produits en un seul : un journal consacré au cinéma, des discussions, une messagerie en temps réel, des événements et des recommandations basées sur l’IA. Je le développe en solo et il doit fonctionner en production à un coût raisonnable, tout en restant facile à comprendre.

## Options considered

EN:

- Microservices from day one: strong isolation, but heavy operational cost (deployments, network calls, distributed data) for me.
- Classic monolith with no internal boundaries: fastest start, but modules end up tangled and impossible to extract later.
- Modular monolith: one deployable application split into modules with strict boundaries, extracting a service only when a metric justifies it.

FR:

- Microservices dès le départ : isolation forte, mais coût opérationnel élevé (déploiements, appels réseau, données distribuées) pour moi.
- Monolithe classique sans frontières internes : démarrage plus rapide, mais les modules finissent par s’emmêler et deviennent impossibles à extraire par la suite.
- Monolithe modulaire : une seule application déployable divisée en modules aux frontières strictes, l’extraction d’un service n’étant effectuée que lorsqu’un indicateur le justifie.

## Decision

EN:
I build a modular monolith of ten modules, each owning its own tables, plus a real-time gateway deployed separately from phase 2.

FR:
Je construit un monolithe modulaire composé de dix modules, chacun disposant de ses propres tables, ainsi qu’une passerelle en temps réel déployée séparément à partir de la phase 2.

## Consequences

EN:

- Easier: one codebase, one deployment, local transactions, simple debugging.
- Harder: boundaries must be enforced by convention and by an automated architecture test.
- Rules: a module never writes to another module's tables; it calls its public interface or reacts to its events.
- To watch: Messaging and AI are the extraction candidates. Each extraction gets its own ADR, backed by a measured reason (concurrent connections, AI cost or latency).

FR:

- Plus simple : une seule base de code, un seul déploiement, des transactions locales, un débogage simple.
- Plus difficile : les limites doivent être respectées par convention et par un test d’architecture automatisé.
- Règles : un module n’écrit jamais dans les tables d’un autre module ; il appelle son interface publique ou réagit à ses événements.
- À surveiller : la messagerie et l’IA sont les candidats à l’extraction. Chaque extraction fait l’objet d’un ADR spécifique, étayé par une raison mesurable (connexions simultanées, coût de l’IA ou latence).
