# 0009 — Transactional outbox for domain events, message broker later

- Status: accepted
- Date: 2026-11-18

## Context

EN:
When something happens (a review is published), other work must follow: notifications, counters, feed entries, moderation, AI profile updates. This work must never be lost, and must never block the main action.

FR:
Quand un événement se produit (une critique est publiée), d'autres traitements doivent suivre : notifications, compteurs, entrées du fil, modération, mise à jour du profil IA. Ces traitements ne doivent jamais être perdus, ni bloquer l'action principale.

## Options considered

EN:

- Direct calls in the request: simple, but slow and fragile; one failure breaks the user action.
- Transactional outbox + workers: events are written to an `outbox` table in the same transaction as the data, then processed by workers. No extra infrastructure.
- Dedicated message broker (RabbitMQ, NATS, Kafka): more features (replay, throughput, many consumers), but one more system to run.

FR:

- Appels directs dans la requête : simple, mais lent et fragile ; un seul échec casse l'action de l'utilisateur.
- Outbox transactionnelle + workers : les événements sont écrits dans une table `outbox` dans la même transaction que la donnée, puis traités par des workers. Aucune infrastructure supplémentaire.
- Broker de messages dédié (RabbitMQ, NATS, Kafka) : plus de fonctionnalités (rejeu, débit, consommateurs multiples), mais un système de plus à exploiter.

## Decision

EN:
I use a transactional outbox processed by workers in the MVP, and add a message broker deployed on Kubernetes in phase 2, fed by the same outbox.

FR:
J'utilise une outbox transactionnelle traitée par des workers dans le MVP, et j'ajouterai un broker de messages déployé sur Kubernetes en phase 2, alimenté par la même outbox.

## Consequences

EN:

- Easier: no event is lost if the database commit succeeds; no extra infrastructure at first.
- Harder: consumers must be idempotent, since an event can be delivered more than once.
- Failed events go to a visible dead-letter list after retries with backoff.
- The outbox stays after the broker arrives: it is what guarantees reliable publishing.

FR:

- Avantages : aucun événement n'est perdu si le commit en base réussit ; aucune infrastructure supplémentaire au départ.
- Inconvénients : les consommateurs doivent être idempotents, car un événement peut être livré plusieurs fois.
- Les événements en échec passent dans une file d'échecs visible, après plusieurs tentatives avec délai croissant.
- L'outbox reste en place après l'arrivée du broker : c'est elle qui garantit une publication fiable.
