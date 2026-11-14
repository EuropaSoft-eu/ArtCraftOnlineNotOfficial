# Suivi du projet ArtCraft Apps Online

Mémoire du projet : à lire avant de reprendre le travail, à compléter après chaque modification.

## Principe

- Le dépôt ne contient pas les apps. `build.py` télécharge la dernière release web de chaque dépôt `storytold/<app>` (liste dans `apps.json`) et génère le site.
- `.github/workflows/publier.yml` publie sur GitHub Pages depuis `main` : à chaque push, à la main, et toutes les 3 heures si une app a changé (`build.py --check` compare `versions.json` du site aux releases).
- Les tâches planifiées GitHub sont irrégulières : écarts constatés de 4 à 13 heures entre deux vérifications.
- Page d'accueil : `template/index.html` (jetons `{{CARDS}}`, `{{DATE}}`, `{{DATE_ISO}}`). Service worker : `template/sw.js`.
- Version et journal des changements du site : `AppInfo.json`.

## Tester en local

`python3 build.py --out _site --zips DOSSIER` avec des zips nommés `<repo>-web-<version>.zip` (sans accès à `gh`, les icônes officielles sont remplacées par les icônes de secours).

## Historique

| Date | Version | Changement |
|---|---|---|
| 2026-11-14 | 1.6 | Nom « ArtCraft Apps Online », signature « par EuropaSoft » avec logo (fichiers `template/europasoft-logo*.webp`, repris du dépôt `EuropaSoft_SiteWeb_Prod`). |
| 2026-11-14 | 1.5 | Date et heure de dernière mise à jour (heure de Paris) à côté du titre ; cache de l'accueil renouvelé à chaque publication. |
| 2026-10-29 | 1.4 | Nom « Craft Apps Online », avertissement site non officiel. |
| 2026-10-28/29 | 1.0 à 1.3 | Voir `AppInfo.json`. |
