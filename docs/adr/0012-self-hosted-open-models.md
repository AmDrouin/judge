# 0012 — Self-hosted open models for AI features

- Status: accepted
- Date: 2026-11-18

## Context

EN:
Phase 3 needs two kinds of models: embedding models (text and image) for search, and a conversational model with tool calling for the recommendation agent.

FR:
La phase 3 a besoin de deux types de modèles : des modèles d'embeddings (texte et image) pour la recherche, et un modèle conversationnel capable d'appeler des outils pour l'agent de recommandation.

## Options considered

EN:

- Hosted model APIs: best quality with no infrastructure, but per-request cost, dependency on a vendor, and less learning.
- Self-hosted open models: control and independence; embedding models run fine on CPU, but a conversational model needs a GPU to answer fast.

FR:

- API de modèles hébergés : la meilleure qualité sans infrastructure, mais un coût par requête, une dépendance à un fournisseur et moins d'apprentissage.
- Modèles ouverts auto-hébergés : maîtrise et indépendance ; les modèles d'embeddings tournent bien sur CPU, mais un modèle conversationnel a besoin d'un GPU pour répondre vite.

## Decision

EN:
I use open models: embedding models hosted on my Kubernetes cluster, and the agent's conversational model on a GPU or through an inference host serving open models.

FR:
J'utilise des modèles ouverts : les modèles d'embeddings hébergés sur mon cluster Kubernetes, et le modèle conversationnel de l'agent sur un GPU ou via un hébergeur d'inférence qui sert des modèles ouverts.

## Consequences

EN:

- Easier: no lock-in, full control over data and versions.
- Harder: the GPU is the main cost item; model serving, scaling and updates are on me.
- The agent may only cite films returned by its tools, and user content is always treated as data, never as instructions.
- To watch: cost and latency per request, logged and capped per plan; quality measured on an annotated evaluation set, in French.

FR:

- Avantages : aucune dépendance à un fournisseur, maîtrise complète des données et des versions.
- Inconvénients : le GPU est le principal poste de coût ; le service des modèles, leur montée en charge et leurs mises à jour sont à ma charge.
- L'agent ne peut citer que des films renvoyés par ses outils, et le contenu des utilisateurs est toujours traité comme une donnée, jamais comme une instruction.
- À surveiller : le coût et la latence par requête, journalisés et plafonnés selon l'abonnement ; la qualité mesurée sur un jeu d'évaluation annoté, en français.
