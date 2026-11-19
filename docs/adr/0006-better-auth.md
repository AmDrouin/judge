# 0006 — Better Auth for authentication, wrapped in the Identity module

- Status: accepted
- Date: 2026-11-19

## Context

EN:
Judge needs sign-up, login, email verification, password reset and social login, in production, with real users. Writing authentication from scratch is risky; delegating it entirely to a hosted service teaches little and creates a dependency.

FR:
Judge a besoin de l'inscription, de la connexion, de la vérification d'email, de la réinitialisation du mot de passe et de la connexion sociale, en production, avec de vrais utilisateurs. Écrire l'authentification de zéro est risqué ; la déléguer entièrement à un service hébergé apprend peu et crée une dépendance.

## Options considered

EN:

- Better Auth: the reference TypeScript auth library; Auth.js is now maintained by the same team, which recommends Better Auth for new projects. Plugins for 2FA, passkeys and organizations; Drizzle adapter. NestJS integration is community maintained.
- Passport.js + custom code: classic with NestJS and instructive, but email verification, password reset and sessions must be written by hand: a large surface for security bugs.
- Keycloak: a complete identity server deployable on Kubernetes, but heavy and oversized for a consumer app; its official Node.js adapter is deprecated.
- Hosted provider (Auth0, Clerk): no work, but no learning and vendor lock-in.

FR:

- Better Auth : la bibliothèque d'authentification TypeScript de référence ; Auth.js est désormais maintenu par la même équipe, qui recommande Better Auth pour les nouveaux projets. Plugins pour la 2FA, les passkeys et les organisations ; adaptateur Drizzle. L'intégration NestJS est maintenue par la communauté.
- Passport.js + code maison : classique avec NestJS et formateur, mais la vérification d'email, la réinitialisation du mot de passe et les sessions sont à écrire à la main : une grande surface pour des failles de sécurité.
- Keycloak : un serveur d'identité complet, déployable sur Kubernetes, mais lourd et surdimensionné pour une application grand public ; son adaptateur Node.js officiel est déprécié.
- Fournisseur hébergé (Auth0, Clerk) : aucun travail, mais aucun apprentissage et une dépendance au fournisseur.

## Decision

EN:
I use Better Auth with its Drizzle adapter, wrapped in my own Identity module.

FR:
J'utilise Better Auth avec son adaptateur Drizzle, enveloppé dans mon propre module Identité.

## Consequences

EN:

- Easier: proven flows (sessions, OAuth, verification) without writing cryptography.
- Rule: the rest of the codebase depends only on the Identity module's interface (`getCurrentUser`, access guards), never on Better Auth directly. Replacing the library would touch one module.
- To watch: the NestJS integration is community maintained and supports Fastify only in beta (see ADR 0003).

FR:

- Avantages : des parcours éprouvés (sessions, OAuth, vérification) sans écrire de cryptographie.
- Règle : le reste du code dépend uniquement de l'interface du module Identité (`getCurrentUser`, gardes d'accès), jamais directement de Better Auth. Remplacer la bibliothèque ne toucherait qu'un seul module.
- À surveiller : l'intégration NestJS est maintenue par la communauté et ne gère Fastify qu'en bêta (voir ADR 0003).
