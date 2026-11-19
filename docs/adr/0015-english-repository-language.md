# 0015 — English for code, bilingual ADRs

- Status: accepted
- Date: 2026-11-19

## Context

EN:
The repository is public and serves as a portfolio. Code identifiers are already in English. Commits, pull requests and documentation could be written in French or in English.

FR:
Le dépôt est public et sert de portfolio. Les identifiants du code sont déjà en anglais. Les commits, les pull requests et la documentation pourraient être écrits en français ou en anglais.

## Options considered

EN:

- French everywhere outside the code: natural for me, but mixes languages with the code and limits readers.
- English everywhere in the repository: consistent with the code, readable by any recruiter or contributor, good practice of written technical English.
- English, with a French version of the ADRs: the same benefits, while keeping the reasoning easy for me to reread and explain in French.

FR:

- Français partout en dehors du code : naturel pour moi, mais mélange les langues avec le code et limite le nombre de lecteurs.
- Anglais partout dans le dépôt : cohérent avec le code, lisible par n'importe quel recruteur ou contributeur, bon entraînement à l'anglais technique écrit.
- Anglais, avec une version française des ADR : les mêmes avantages, tout en gardant un raisonnement facile à relire et à expliquer en français.

## Decision

EN:
Code, commits, branches, pull requests and the README are written in English. ADRs are written in English with a French version under each section. The app's user interface is French first. My personal learning journal (`docs/journal.md`) may stay in French.

FR:
Le code, les commits, les branches, les pull requests et le README sont écrits en anglais. Les ADR sont écrits en anglais, avec une version française sous chaque section. L'interface de l'application est d'abord en français. Mon journal d'apprentissage personnel (`docs/journal.md`) peut rester en français.

## Consequences

EN:

- Easier: one main language in the repository; the project can be shown anywhere; ADRs stay accessible to French-speaking readers.
- Harder: writing takes a bit more effort, and both versions of an ADR must be kept in sync when it changes.
- The first commit (`chore: initialise le monorepo`) predates this decision and stays as is; history is not rewritten.

FR:

- Avantages : une langue principale dans le dépôt ; le projet peut être montré partout ; les ADR restent accessibles aux lecteurs francophones.
- Inconvénients : la rédaction demande un peu plus d'effort, et les deux versions d'un ADR doivent rester alignées quand il évolue.
- Le premier commit (`chore: initialise le monorepo`) est antérieur à cette décision et reste tel quel ; l'historique n'est pas réécrit.
