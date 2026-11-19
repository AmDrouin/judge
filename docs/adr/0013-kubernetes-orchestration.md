# 0013 — Kubernetes for orchestration

- Status: accepted
- Date: 2026-11-18

## Context

EN:
Judge runs several processes (API, web app, workers, real-time gateway, later AI services) that must be deployed, scaled and updated without downtime. Mastering Kubernetes is an explicit learning goal of the project.

FR:
Judge fait tourner plusieurs processus (API, application web, workers, gateway temps réel, puis services IA) qui doivent être déployés, mis à l'échelle et mis à jour sans interruption. Maîtriser Kubernetes est un objectif d'apprentissage explicite du projet.

## Options considered

EN:

- Managed container platform (PaaS): simplest and cheapest to run, less to learn.
- Kubernetes: industry standard, strong career signal, fixed cost and real operational complexity.

FR:

- Plateforme de conteneurs managée (PaaS) : la plus simple et la moins chère à exploiter, moins à apprendre.
- Kubernetes : standard de l'industrie, fort signal sur un CV, coût fixe et vraie complexité d'exploitation.

## Decision

EN:
I use Kubernetes: a local cluster (k3d) from phase 0, and a managed cluster in production, deployed with Helm charts and Argo CD (GitOps).

FR:
J'utilise Kubernetes : un cluster local (k3d) dès la phase 0, et un cluster managé en production, déployé avec des charts Helm et Argo CD (GitOps).

## Consequences

EN:

- Easier: one model for every environment; rolling updates, probes, autoscaling.
- Harder: manifests, ingress, certificates, secrets and cluster costs must be managed.
- Production PostgreSQL stays on the provider's managed database (automatic backups) rather than in the cluster.
- To watch: monthly cost of the cluster. Compare providers (cluster price, managed database, EU data location) in a dedicated ADR at phase 0, step 10.

FR:

- Avantages : un seul modèle pour tous les environnements ; mises à jour progressives, sondes de santé, mise à l'échelle automatique.
- Inconvénients : manifestes, ingress, certificats, secrets et coût du cluster sont à gérer.
- En production, PostgreSQL reste sur la base managée du fournisseur (sauvegardes automatiques) plutôt que dans le cluster.
- À surveiller : le coût mensuel du cluster. Comparer les fournisseurs (prix du cluster, base managée, hébergement des données dans l'UE) dans un ADR dédié à l'étape 10 de la phase 0.
