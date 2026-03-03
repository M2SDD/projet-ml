# Prédiction des revenus — Adult Dataset

**Projet Machine Learning — M2 SDD**

*Matthieu PELINGRE*

---

## Objectif

Prédire si le revenu annuel d'un individu dépasse **50 000 $** à partir de données socio-démographiques issues du recensement américain de 1994 ([Adult / Census Income Dataset](https://doi.org/10.24432/C5XW20), UCI ML Repository).

Il s'agit d'une tâche de **classification binaire supervisée** sur 48 842 individus décrits par 14 variables (6 numériques, 8 catégorielles).

---

## Livrables

| Livrable | Lien |
|---|---|
| Notebook d'analyse | [projet-machine_learning.ipynb](projet-machine_learning.ipynb) |
| Rapport PDF | [rapport/rapport.pdf](rapport/rapport.pdf) |

---

## Structure du projet

```
.
├── projet-machine_learning.ipynb   # Notebook principal (analyse complète)
├── rapport/
│   ├── rapport.tex                 # Source LaTeX du rapport
│   └── rapport.pdf                 # Rapport de modélisation
├── data/                           # Jeu de données Adult (UCI)
├── figures/                        # Visualisations générées
├── models/                         # Modèles entraînés sauvegardés
├── UNSD_M49_Standard_Region_Codes.csv  # Référentiel géographique ONU M49
├── requirements.txt                # Dépendances Python
└── requirements_versions.txt       # Dépendances avec versions fixées
```

---

## Contenu du notebook

1. **Chargement des données** — import via `ucimlrepo`
2. **Description et nettoyage** — gestion des valeurs manquantes (MNAR/MCAR), suppression des variables redondantes (`education`, `fnlwgt`), regroupement géographique (`native-country` → `native-subregion`, standard M49 ONU)
3. **Analyse exploratoire (EDA)** — distributions, analyse bivariée, corrélations (Spearman, V de Cramér, Eta), information mutuelle, sélection de features
4. **Modélisation** — baseline, preprocessing, Random Forest, XGBoost (optimisation par `GridSearchCV`)
5. **Interprétabilité** — importance des variables
6. **Sauvegarde du modèle** — export du pipeline final
7. **Tests** — simulation de mise en production avec utilisation de SHAP

---

## Résultats

Le modèle retenu est **XGBoost optimisé** :

| **Modèle** | **Acc** | **P** | **R** | **F1-macro** | **AUC-ROC** |
|------------|---------|-------|-------|--------------|-------------|
| DummyClassifier | 0.753 | 0.376 | 0.500 | 0.429 | 0.500 |
| Random Forest | 0.862 | 0.833 | 0.775 | 0.798 | 0.920 |
| **XGBoost** | **0.871** | **0.843** | **0.794** | **0.814** | **0.932** |

---

## Installation

```bash
pip install -r requirements.txt
```

### Dépendances principales

- `scikit-learn`, `xgboost` — modélisation
- `pandas`, `numpy` — manipulation des données
- `matplotlib`, `seaborn` — visualisation
- `shap` — interprétabilité
- `ucimlrepo` — téléchargement du dataset

---

## Données

Le dataset est téléchargé automatiquement depuis l'UCI ML Repository via `ucimlrepo` au lancement du notebook. Les fichiers bruts sont également disponibles dans le dossier [data/](data/).

**Source :** Barry Becker, recensement américain 1994.
**DOI :** [10.24432/C5XW20](https://doi.org/10.24432/C5XW20)