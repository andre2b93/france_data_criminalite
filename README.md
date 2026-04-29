# France — Données de Criminalité

Portail de tableaux de bord interactifs analysant la criminalité en France et sa relation avec l'immigration sur la période **2016–2024** (avec quelques séries longues remontant à 2000). Le dépôt est composé exclusivement de fichiers HTML statiques utilisant **Chart.js** pour les graphiques et **D3.js** pour les cartes choroplèthes.

## Comment consulter

### En ligne (recommandé — fonctionne aussi sur mobile)

Une fois GitHub Pages activé sur ce dépôt, le portail est accessible à :

```
https://andre2b93.github.io/france_data_criminalite/
```

Il suffit d'ouvrir cette URL dans un navigateur (Firefox, Chrome, Safari, mobile ou desktop). `index.html` redirige automatiquement vers `portail_analyse.html`.

#### Activer GitHub Pages (à faire une fois)

1. Sur GitHub, ouvrir **Settings → Pages**.
2. Sous **Source**, choisir **Deploy from a branch**.
3. Sélectionner la branche `main` et le dossier `/ (root)`, puis **Save**.
4. Attendre ~1 minute, puis rafraîchir : l'URL ci-dessus devient active.

#### Sur Firefox Android — installer comme une appli

1. Ouvrir l'URL ci-dessus dans Firefox sur Android.
2. Menu **⋮** → **Installer** (ou **Ajouter à l'écran d'accueil**).
3. Une icône apparaît sur l'écran d'accueil ; un tap ouvre directement le portail en plein écran.

Le manifeste PWA (`manifest.webmanifest`) et l'icône (`icon.svg`) sont déjà fournis dans le dépôt.

### En local

Aucun build, aucune dépendance à installer. Ouvrir directement `portail_analyse.html` dans un navigateur :

```
# depuis la racine du dépôt
xdg-open portail_analyse.html   # Linux
open portail_analyse.html       # macOS
start portail_analyse.html      # Windows
```

## Tableaux de bord

### Criminalité

- **`criminalite_france_dashboard.html`** — Tendances nationales des crimes et délits (2000–2021) par catégorie : vols, violences, cambriolages, usage de stupéfiants, escroqueries, violences sexuelles. Inclut taux départementaux, condamnations et population carcérale.
- **`criminalite_nationalite_complet.html`** — Vue d'ensemble de la criminalité par nationalité : part des mis en cause étrangers, victimes, et **Indice de Surreprésentation (ISR)**.
- **`nationalite_dashboard.html`** — Répartition par nationalité des personnes incarcérées et mises en cause ; comparaison démographie carcérale (≈ 23,7 % d'étrangers, 60,5 % d'origine africaine) avec les statistiques SSMSI.

### Immigration × Criminalité

- **`dashboard_mec_nationalite.html`** — Analyse ISR détaillée des **mis en cause** par nationalité sur 17 indicateurs de criminalité, avec tableaux triables.
- **`dashboard_isr_criminalite_immigration.html`** — Évolution de l'**ISR 2016–2024** par catégorie d'infraction : quels types d'infractions présentent une participation étrangère élevée.
- **`dashboard_mise_en_relation.html`** — Corrélation entre flux migratoires (titres de séjour délivrés) et taux de criminalité. Coefficient rapporté : **r = +0,85 (p = 0,016)** hors anomalie COVID 2020.
- **`dashboard_chaine_penale.html`** — Suivi de la **chaîne pénale** : interpellation → condamnation → incarcération. Graphiques double axe et analyse en entonnoir.
- **`dashboard_phase4.html`** — Tableau de bord intégrateur « Phase 4 » combinant flux migratoires, criminalité, condamnations et population carcérale, avec sélecteur d'année.

### Géographie

- **`dashboard_cartes_phase4.html`** — Cartes choroplèthes départementales (D3.js) des taux de criminalité et indicateurs associés.

## Sources de données

| Source | Couverture |
|---|---|
| **SSMSI** | Statistiques de la délinquance enregistrée par police et gendarmerie |
| **INSEE** | Démographie, part de la population étrangère |
| **CJN / SDSE** | Casier judiciaire national, condamnations |
| **DAP** | Direction de l'administration pénitentiaire — population carcérale |
| **DGEF** | Direction générale des étrangers en France — titres de séjour, flux migratoires |

## Notes méthodologiques

- **Granularité « nationalité » limitée.** Le SSMSI ne distingue dans ses publications ouvertes que **français / étrangers** (binaire). Les analyses par nationalité fine sur la chaîne pénale relèvent donc d'estimations, signalées comme telles dans les tableaux de bord concernés.
- **ISR (Indice de Surreprésentation)** = part des mis en cause étrangers rapportée au poids démographique des étrangers. Un ISR > 1 indique une surreprésentation, < 1 une sous-représentation. À interpréter avec précaution (composition d'âge, de sexe, de territoire non contrôlée).
- **Corrélation ≠ causalité.** La corrélation forte rapportée dans `dashboard_mise_en_relation.html` ne préjuge pas d'un lien de cause à effet ; les avertissements sont rappelés dans les tableaux de bord.
- **Anomalie 2020.** Les confinements COVID-19 ont fortement perturbé les séries de flux migratoires et de criminalité enregistrée ; certaines analyses excluent explicitement cette année.

## Pile technique

- HTML statique, aucun build, aucune dépendance à installer.
- **Chart.js** (chargé via CDN) pour les graphiques en ligne, barres et secteurs.
- **D3.js** (chargé via CDN) pour les cartes choroplèthes.
- Filtres interactifs côté client (sélection d'année, de catégorie, tris de tableaux).
- **PWA minimal** (`manifest.webmanifest` + `icon.svg`) pour l'installation sur l'écran d'accueil mobile via Firefox Android / Chrome.

## Structure du dépôt

```
index.html                 → redirection vers portail_analyse.html
portail_analyse.html       → page d'accueil (navigation latérale)
*_dashboard.html, dashboard_*.html, criminalite_*.html, nationalite_dashboard.html
                           → 9 tableaux de bord
manifest.webmanifest       → manifeste PWA (installation mobile)
icon.svg                   → icône du portail / de la PWA
```
