# 0010 — WebSocket for real-time features

- Status: accepted
- Date: 2026-11-18

## Context

EN:
Private messaging, group chats and 24-hour film rooms need instant, two-way communication: messages, presence and typing indicators.

FR:
La messagerie privée, les discussions de groupe et les salons de film de 24 heures ont besoin d'une communication instantanée dans les deux sens : messages, présence et indicateurs de saisie.

## Options considered

EN:

- WebSocket: two-way, low latency, one persistent connection; stateful connections are harder to scale.
- Server-Sent Events + HTTP requests: simpler and auto-reconnecting, but server-to-client only.
- Managed real-time service: no operations work, but cost and less learning.

FR:

- WebSocket : bidirectionnel, faible latence, une seule connexion persistante ; les connexions avec état sont plus difficiles à faire monter en charge.
- Server-Sent Events + requêtes HTTP : plus simple et avec reconnexion automatique, mais uniquement du serveur vers le client.
- Service temps réel managé : aucune exploitation, mais un coût et moins d'apprentissage.

## Decision

EN:
I use WebSocket, served by a dedicated real-time gateway (ADR 0001).

FR:
J'utilise WebSocket, servi par un gateway temps réel dédié (ADR 0001).

## Consequences

EN:

- Easier: chat, presence and typing indicators.
- Harder: horizontal scaling needs a pub/sub layer between gateway instances; reconnection and message backfill ("since last id") are mine to implement.
- Authentication goes through a cookie or a token at connection time, since browsers cannot set headers on WebSocket.
- To watch: ingress timeouts and connection draining during Kubernetes deployments.

FR:

- Avantages : chat, présence et indicateurs de saisie.
- Inconvénients : la montée en charge horizontale nécessite une couche pub/sub entre les instances du gateway ; la reconnexion et la récupération des messages manqués (« depuis le dernier id ») sont à implémenter moi-même.
- L'authentification passe par un cookie ou un jeton à la connexion, car les navigateurs ne permettent pas d'ajouter des en-têtes à une connexion WebSocket.
- À surveiller : les délais d'expiration de l'ingress et la fermeture propre des connexions pendant les déploiements Kubernetes.
