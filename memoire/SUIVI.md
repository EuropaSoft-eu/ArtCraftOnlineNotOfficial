# Suivi du projet ArtCraft Apps Online

Mémoire du projet : à lire avant de reprendre le travail, à compléter après chaque modification.

## Principe

- Le dépôt ne contient pas les apps. `build.py` télécharge la dernière release web de chaque dépôt `storytold/<app>` (liste dans `apps.json`) et génère le site.
- `.github/workflows/publier.yml` publie sur GitHub Pages depuis `main` : à chaque push, à la main, et toutes les 3 heures si une app a changé (`build.py --check` compare `versions.json` du site aux releases).
- Les tâches planifiées GitHub sont irrégulières : écarts constatés de 4 à 13 heures entre deux vérifications.
- Page d'accueil : `template/index.html` (jetons `{{CARDS}}`, `{{DATE}}`, `{{DATE_ISO}}`, `{{REPO}}`). Service worker : `template/sw.js`.
- Version et journal des changements du site : `AppInfo.json`.

## Adresses

- Dépôt : `EuropaSoft-eu/ArtCraftOnlineNotOfficial` (renommé le 14/11/2026, ancien nom `craft`).
- Site : https://europasoft-eu.github.io/ArtCraftOnlineNotOfficial/ (l'ancienne adresse `/craft/` répond 404 ; la casse compte).
- L'adresse du site est en dur dans `publier.yml` (`SITE_URL`), `README.md` et `AppInfo.json` : à corriger à chaque renommage, sinon la vérification planifiée ne trouve plus `versions.json` et reconstruit à chaque passage.

## Tester en local

`python3 build.py --out _site --zips DOSSIER` avec des zips nommés `<repo>-web-<version>.zip` (sans accès à `gh`, les icônes officielles sont remplacées par les icônes de secours).

## Historique

| Date | Version | Changement |
|---|---|---|
| 2026-11-21 | 1.9 | Heure de la dernière vérification affichée (JS : API GitHub, dernier run réussi de `publier.yml` ; jeton `{{REPO}}` rempli par `GITHUB_REPOSITORY`). Vérif. 21/11 12h11 : 15 apps à jour. |
| 2026-11-20 | 1.8 | TextureCraft et MaterialCraft ajoutées (`apps.json`). |
| 2026-11-20 | 1.7 | Texte à côté du titre : « Dernière mise à jour faite le … ». |
| 2026-11-14 | 1.6 | Nom « ArtCraft Apps Online », signature « par EuropaSoft » avec logo (fichiers `template/europasoft-logo*.webp`, repris du dépôt `EuropaSoft_SiteWeb_Prod`). |
| 2026-11-14 | 1.5 | Date et heure de dernière mise à jour (heure de Paris) à côté du titre ; cache de l'accueil renouvelé à chaque publication. |
| 2026-10-29 | 1.4 | Nom « Craft Apps Online », avertissement site non officiel. |
| 2026-10-28/29 | 1.0 à 1.3 | Voir `AppInfo.json`. |

## Vérifications ponctuelles

- 21/11/2026 à 12h11 (Paris) : 15/15 apps à jour sur le site (pdf 0.21.1, word 0.18.1, grid 0.19.1, deck 0.18.1, photo 0.23.1, light 0.21.1, vector 0.24.1, design 0.20.1, fig 0.18.1, film 0.20.1, effect 0.24.1, sound 0.20.1, cad 0.20.1, texture 0.6.1, material 0.4.1).
- L'affichage de l'heure de vérification (1.9) n'est visible qu'une fois fusionné dans `main`.
