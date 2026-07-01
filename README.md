# 📊 Dashboard Ventes — Sample Superstore (Power BI)

## 🎯 Contexte et objectif

Ce projet a été réalisé dans le cadre de ma préparation à une alternance en Data Analyse, pour mettre en pratique mes compétences sur un outil de Business Intelligence professionnel.

Le dataset **Sample Superstore** contient les données de ventes d'une entreprise de e-commerce américaine (commandes, produits, clients, régions, dates, ventes, profits, remises).

**Objectif business :** analyser la performance commerciale de l'entreprise afin d'identifier :
- les tendances de ventes dans le temps (saisonnalité),
- les catégories de produits les plus rentables,
- les zones géographiques les plus performantes,
- les leviers d'amélioration de la marge.

## 🛠️ Étapes techniques

### 1. Nettoyage des données (Power Query)
- Import du fichier source et correction des types de colonnes (dates au format anglais MM/JJ/AAAA converties via la locale, valeurs numériques)
- Vérification et suppression des doublons
- Contrôle des valeurs manquantes via l'aperçu qualité des données
- Création d'une colonne calculée `Marge` (`Profit / Sales`)

### 2. Modélisation des données
- Construction d'un **modèle en étoile** : table de faits `Sample_Superstore` reliée à une table de dimension `Calendrier`
- Table `Calendrier` créée en DAX (`CALENDAR()`) avec colonnes `Année`, `Mois`, `NumMois` (pour le tri chronologique)
- Relation établie entre `Calendrier[Date]` et `Sample_Superstore[Order Date]`

### 3. Mesures DAX
| Mesure | Formule | Description |
|---|---|---|
| CA Total | `SUM(Sales)` | Chiffre d'affaires total |
| Profit Total | `SUM(Profit)` | Profit total |
| Marge % | `DIVIDE([Profit Total],[CA Total],0)` | Marge en pourcentage |
| CA Année Précédente | `CALCULATE([CA Total], SAMEPERIODLASTYEAR(...))` | Comparaison année sur année |

### 4. Visualisations et interactivité
- 3 cartes KPI (CA Total, Profit Total, Marge %)
- Graphique en courbes : évolution mensuelle du CA, une couleur par année
- Graphique en barres : répartition du CA par catégorie de produits
- Carte géographique : répartition des ventes par pays/ville
- Segments (slicers) interactifs : Année, Catégorie, Région

## 💡 Insights clés

1. **Saisonnalité marquée** : les ventes atteignent systématiquement un pic en fin d'année (novembre-décembre), probablement lié aux périodes de fêtes et promotions type Black Friday.
2. **Technology est la catégorie la plus performante**, avec un CA de 836,15 K$ et une marge de 0,17 %, contre 742,00 K$ de CA pour Furniture qui n'affiche qu'une marge de 0,02 %. Furniture génère donc presque autant de chiffre d'affaires que Technology, mais avec une rentabilité près de 8 fois inférieure — un signal pour investiguer les remises accordées ou les coûts associés à cette catégorie.
3. **La région West domine en volume et en rentabilité** : elle génère le CA le plus élevé (725,46 K$) avec la meilleure marge (0,15 %), quasiment le double du CA de la région South (391,92 K$, marge de 0,12 %). Cela suggère que West bénéficie soit d'une base clients plus large, soit d'une politique de remises plus maîtrisée que dans le Sud.

## 📈 Compétences mobilisées
`Power BI` `Power Query` `DAX` `Modélisation de données` `Data Visualisation` `Analyse business`

## 📁 Contenu du repo
- `dashboard_superstore.pbix` — fichier Power BI source
- `screenshots/` — captures d'écran du dashboard (vue globale + exemples de filtres appliqués)

## 👤 Auteure
Mathilde Bassadou — Étudiante en M1 MIAGE, Université de Rennes
[LinkedIn](https://www.linkedin.com/in/mathilde-bassadou-504954256/) · [GitHub](https://github.com/Mathilde4)
