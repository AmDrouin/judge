# 0014 — Self-hosted open-source observability stack

- Status: accepted
- Date: 2026-11-18

## Context

EN:
I need logs, metrics and traces to run Judge in production, and a super-admin dashboard showing API response times and recent errors.

FR:
J'ai besoin de logs, de métriques et de traces pour exploiter Judge en production, ainsi que d'un tableau de bord super-admin affichant les temps de réponse de l'API et les erreurs récentes.

## Options considered

EN:

- Self-hosted stack on the cluster (Prometheus, Grafana, Loki, Tempo): free licences, industry standard, great Kubernetes learning; uses cluster memory and needs maintenance.
- SaaS offering (Grafana Cloud, Datadog): nothing to maintain, better UX; limited free tiers, expensive at scale, less learning.

FR:

- Stack auto-hébergée sur le cluster (Prometheus, Grafana, Loki, Tempo) : licences gratuites, standard de l'industrie, excellent apprentissage de Kubernetes ; consomme de la mémoire du cluster et demande de la maintenance.
- Offre SaaS (Grafana Cloud, Datadog) : rien à maintenir, meilleure ergonomie ; offres gratuites limitées, coûteuse à grande échelle, moins d'apprentissage.

## Decision

EN:
I self-host an open-source observability stack on the cluster, and instrument the code with an open standard (OpenTelemetry).

FR:
J'auto-héberge une stack d'observabilité open source sur le cluster, et j'instrumente le code avec un standard ouvert (OpenTelemetry).

## Consequences

EN:

- Easier: full control, no per-volume bill; the admin dashboard reads from the same data.
- Harder: the stack needs memory and upgrades; retention must be configured.
- Logs are structured JSON (Pino) with a request id, and never contain message content or email addresses.
- Because instrumentation follows an open standard, moving to a SaaS later would not require code changes.

FR:

- Avantages : maîtrise complète, aucune facture au volume ; le tableau de bord admin lit les mêmes données.
- Inconvénients : la stack demande de la mémoire et des mises à jour ; la durée de rétention doit être configurée.
- Les logs sont en JSON structuré (Pino) avec un identifiant de requête, et ne contiennent jamais le contenu des messages ni d'adresses email.
- Comme l'instrumentation suit un standard ouvert, passer plus tard à un SaaS ne demanderait aucune modification du code.
