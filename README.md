# Russian Learning Content

Contenu JSON pour une future application personnelle d'apprentissage du russe.

## v0.2.0 — corpus consolidé

Cette version fusionne :

- le socle adaptatif créé pour la future app ;
- les mécaniques pédagogiques déjà testées dans `russian-morning-app` ;
- le corpus du PDF **Première semaine de Tony en Russie**.

Le dépôt sépare volontairement le **contenu disponible** du **contenu à servir maintenant**. Les notions adaptées au flux actuel sont `active`; les sujets un peu plus avancés (restaurant, hôtel, certaines prépositions) sont déjà présents mais classés `preview`.

## Principes

- aucun recours à la translittération ;
- russe en cyrillique ;
- contexte avant analyse grammaticale exhaustive ;
- compréhension globale des lectures ;
- distracteurs proches et plausibles ;
- rappel de formes et de lemmes ;
- traduction active ;
- erreur décrite par `error_tags`, pas seulement par un score faux/vrai ;
- accents toniques acceptés mais jamais exigés dans la saisie ;
- une difficulté fréquente doit revenir dans **de nouvelles phrases**, pas seulement dans le même exercice.

## Structure

```text
.
├── manifest.json
├── normalization.json
├── error-taxonomy.json
├── practice-series.json
├── courses/
│   ├── 01-foundations/
│   ├── 02-core-grammar/
│   ├── 03-reading/
│   └── 04-practice/
├── exercises/
│   ├── 01-foundations/
│   ├── 02-core-grammar/
│   ├── 03-reading/
│   └── 04-practice/
├── vocabulary/
├── sources/
│   ├── github/
│   └── pdf/
├── schemas/
└── scripts/
```

## Synchronisation prévue

L'application télécharge `manifest.json`, compare `content_version`, puis met en cache les fichiers référencés.

GitHub contient les cours. Firebase doit contenir l'état de l'apprenant : tentatives, erreurs, historique, maîtrise estimée et révisions.

## Moteur adaptatif de départ

Le manifest recommande :

- 40 % progression normale ;
- 35 % erreurs récentes ;
- 20 % révision espacée ;
- 5 % traduction active.

Une erreur fréquente reçoit un boost, mais le même exercice a un cooldown de plusieurs sessions. Le moteur doit préférer **même concept + autre phrase**.

## Validation

```bash
python scripts/validate_content.py
```
