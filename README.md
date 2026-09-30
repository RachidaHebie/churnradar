# 📊 Analyse du Churn Client — Telco Customer Churn

Projet d'analyse de données réalisé dans le cadre du cours **EECE 231 – Data Science (Part II)**.

**Auteure :** Tié Rachida HEBIE

---

## 🎯 Objectif du projet

La rétention client est un enjeu majeur pour les entreprises de télécommunications, où le coût d'acquisition d'un nouveau client est généralement bien plus élevé que celui de la fidélisation d'un client existant.

Ce projet analyse un jeu de données de **7 043 clients** d'une entreprise de télécommunications fictive afin de répondre à la question suivante :

> **Quels sont les facteurs qui influencent le plus la probabilité qu'un client se désabonne (churn), et comment ces facteurs peuvent-ils orienter une stratégie de rétention ?**

---

## 📁 Dataset

- **Nom :** Telco Customer Churn (IBM Sample Dataset)
- **Source :** [Kaggle — blastchar/telco-customer-churn](https://www.kaggle.com/datasets/blastchar/telco-customer-churn)
- **Volume :** 7 043 lignes × 21 colonnes
- **Variable cible :** `Churn` (Yes/No) — 26,5% de taux de désabonnement

---

## 🛠️ Méthodologie

Le projet suit un workflow analytique structuré en plusieurs étapes :

1. **Chargement et aperçu initial** — dimensions, types de variables, structure générale
2. **Diagnostic de qualité** — détection des valeurs manquantes, doublons, statistiques descriptives
3. **Nettoyage et preprocessing** — conversion de `TotalCharges` en numérique, traitement justifié des valeurs manquantes (imputation à 0 pour les clients avec `tenure = 0`)
4. **Analyse exploratoire (EDA)** — analyse univariée et bivariée de chaque variable par rapport au churn, avec visualisations (histogrammes, boxplots, barplots, heatmap de corrélation)
5. **Manipulation et agrégation des données** — tableaux croisés (`crosstab`), tableau pivot (`pivot_table`) pour étudier les effets d'interaction, filtrage de segments à risque
6. **Synthèse et interprétation opérationnelle** — traduction des résultats statistiques en recommandations business
7. **Discussion critique** — limites, hypothèses et biais de l'analyse

---

## 🔍 Principaux résultats

### Facteurs les plus associés au churn

| Facteur | Écart observé |
|---|---|
| Type de contrat | Mensuel : 42,7% vs Deux ans : 2,8% |
| Méthode de paiement | Electronic check : 45,3% vs autres : 15–19% |
| Type de connexion internet | Fibre optique : 41,9% vs Sans internet : 7,4% |
| Absence de sécurité/support en ligne | ~42% vs ~15% avec ces services |
| Ancienneté (tenure) | Médiane 10 mois (churn) vs 38 mois (fidèles) |

### Facteurs sans influence notable

Genre, service téléphonique, lignes multiples, options de streaming — écarts de churn inférieurs à 5 points.

### Découverte clé : un effet d'interaction

Le croisement `Contract` × `InternetService` révèle que les facteurs se renforcent mutuellement plutôt que de s'additionner simplement :

- Contrat 2 ans + Fibre optique → **7,2%** de churn
- Contrat mensuel + Fibre optique → **54,6%** de churn

### Segment client prioritaire identifié

Les clients en **contrat mensuel avec fibre optique** représentent **2 128 clients (30,2% de la base)**, avec un taux de churn de **54,6%** — plus du double de la moyenne générale (26,5%).

---

## 💡 Recommandations opérationnelles

1. **Inciter à l'engagement contractuel** : proposer une migration vers un contrat annuel ou de deux ans, avec avantage tarifaire, en priorité aux clients fibre en contrat mensuel.
2. **Accompagner les nouveaux clients** : renforcer le suivi durant les premiers mois d'abonnement, période où le risque de résiliation est maximal.
3. **Promouvoir les services de protection** : la souscription à la sécurité en ligne et au support technique est associée à une fidélité nettement plus élevée.

---

## ⚠️ Limites de l'analyse

- Le dataset est un échantillon **synthétique** fourni par IBM à des fins pédagogiques, et ne reflète pas nécessairement le comportement réel d'une entreprise de télécommunications.
- Les relations observées sont des **corrélations**, non des relations de cause à effet. La forte corrélation entre `tenure` et `TotalCharges` (0,83) reflète notamment un lien de calcul plutôt qu'un effet explicatif.
- Le dataset ne contient pas de variable temporelle réelle ni d'information contextuelle (concurrence, qualité perçue du service, incidents techniques), qui pourraient pourtant influencer le churn.
- Aucun test de significativité statistique n'a été réalisé sur les écarts observés entre groupes.

---

## 📂 Structure du dépôt

```
churnradar/
├── README.md
├── notebooks/
│   └── telco_churn_analysis.ipynb
├── data/
│   └── WA_Fn-UseC_-Telco-Customer-Churn.csv
└── requirements.txt
```

---

## ⚙️ Reproductibilité

Pour exécuter ce projet localement :

```bash
pip install -r requirements.txt
jupyter notebook notebooks/telco_churn_analysis.ipynb
```

**Librairies utilisées :** pandas, matplotlib, seaborn

---

## 🤖 Usage de l'IA

Ce projet a été réalisé avec l'assistance de Claude (Anthropic) comme outil technique d'aide à la structuration du code, au débogage et à la formulation des interprétations. Voir l'annexe dédiée dans le rapport pour le détail des usages et prompts utilisés, conformément à la politique d'usage de l'IA du cours.
