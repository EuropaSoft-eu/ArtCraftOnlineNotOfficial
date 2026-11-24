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
| 2026-11-24 | 1.11 | Ligne « Dernière vérification des versions officielles le … » : la page lit le dernier passage réussi de `publier.yml` sur l'API GitHub (jeton `{{REPO}}`, repli sur la date de publication). Vérification du 24/11 12h11 Paris : 16 apps à jour ; SolidCraft 0.47.0 en ligne alors que 0.48.1 est sortie le 24/11 05h10 (après le dernier passage planifié, 03h14) : publication relancée à la main. |
| 2026-11-22 | 1.10 | SolidCraft ajoutée (dépôt `tangency-labs/solidcraft`) ; `build.py` accepte un dépôt « propriétaire/nom ». |
| 2026-11-22 | 1.9 | Craft Anything ajoutée (`apps.json`). |
| 2026-11-20 | 1.8 | TextureCraft et MaterialCraft ajoutées (`apps.json`). |
| 2026-11-20 | 1.7 | Texte à côté du titre : « Dernière mise à jour faite le … ». |
| 2026-11-14 | 1.6 | Nom « ArtCraft Apps Online », signature « par EuropaSoft » avec logo (fichiers `template/europasoft-logo*.webp`, repris du dépôt `EuropaSoft_SiteWeb_Prod`). |
| 2026-11-14 | 1.5 | Date et heure de dernière mise à jour (heure de Paris) à côté du titre ; cache de l'accueil renouvelé à chaque publication. |
| 2026-10-29 | 1.4 | Nom « Craft Apps Online », avertissement site non officiel. |
| 2026-10-28/29 | 1.0 à 1.3 | Voir `AppInfo.json`. |

## Routine planifiée « vérifier que les apps sont à jour »

- 2026-11-25 : passage #99 du 25/11 à 09h36 (Paris) réussi, site reconstruit à 09h37 ; versions en ligne dans `versions.json`. Version 1.11 reprise sur `claude/happy-hawking-8vkf5z` ; les branches `claude/happy-hawking-p3duou`, `-byqob2`, `-izynhr` contiennent la même fonctionnalité (doublons, à supprimer après fusion). Tant que la 1.11 n'est pas fusionnée dans `main`, la date de vérification n'apparaît pas sur le site.
