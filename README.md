# PFE-SRM-RSK

## Système intelligent d’analyse de la consommation d’eau et d’électricité

Projet de fin d’études réalisé dans le contexte de la **Société Régionale Multiservices Rabat–Salé–Kénitra (SRM-RSK)**.

L’objectif du projet est de concevoir une chaîne analytique complète permettant d’exploiter les historiques de consommation d’eau et d’électricité afin de :

- prévoir la consommation future ;
- segmenter les clients selon leurs profils ;
- détecter les observations atypiques ;
- classifier les comportements suspects ;
- expliquer les prédictions grâce à l’Explainable AI ;
- construire un score de risque pour prioriser les contrôles ;
- restituer les résultats dans un tableau de bord Power BI.

---

## Architecture générale

La solution est organisée autour de plusieurs briques complémentaires :

1. **Préparation et analyse des données**
   - nettoyage ;
   - traitement des valeurs manquantes ;
   - correction des incohérences ;
   - gestion des valeurs extrêmes ;
   - encodage et standardisation ;
   - feature engineering.

2. **Prévision de la consommation**
   - Random Forest ;
   - XGBoost.

3. **Segmentation des clients**
   - K-Means ;
   - PCA pour la visualisation des profils.

4. **Détection d’anomalies**
   - Isolation Forest ;
   - comparaison avec Local Outlier Factor.

5. **Classification des comportements suspects**
   - Random Forest ;
   - XGBoost ;
   - CatBoost ;
   - gestion du déséquilibre des classes.

6. **Explainable AI**
   - SHAP pour l’explication globale et locale des prédictions.

7. **Score de risque**
   - agrégation de plusieurs signaux afin de hiérarchiser les clients selon leur niveau de priorité.

8. **Business Intelligence**
   - intégration des résultats dans Power BI ;
   - création de KPI et visualisations interactives ;
   - priorisation des clients à contrôler.

---

## Principaux résultats

### Prévision de la consommation

Le modèle **XGBoost** a été retenu comme meilleur modèle de prévision avec :

- **R² : 0,956**
- **MAE : 21,411**
- **RMSE : 36,670**

### Segmentation des clients

La segmentation par **K-Means** a permis d’identifier :

- **4 profils de clients**
- **Coefficient de silhouette : 0,401**

### Détection d’anomalies

L’algorithme **Isolation Forest** a permis d’identifier :

- **1 194 observations atypiques**
- soit environ **2,38 % des relevés**

### Classification des comportements suspects

**XGBoost** a été retenu comme modèle principal pour la classification supervisée en raison de son compromis entre capacité de détection et limitation des fausses alertes.

La problématique étant fortement déséquilibrée, une attention particulière a été portée aux métriques adaptées à la classe minoritaire, notamment :

- précision ;
- rappel ;
- F1-score ;
- PR-AUC ;
- ROC-AUC.

### Explicabilité des prédictions

Les valeurs **SHAP** sont utilisées afin de :

- identifier les variables les plus influentes ;
- comprendre le sens de leur influence ;
- expliquer individuellement certaines prédictions ;
- améliorer la transparence du modèle auprès des utilisateurs métier.

### Score de risque

Les différentes sorties analytiques sont combinées dans un **score de risque compris entre 0 et 100**.

Le score repose sur trois signaux complémentaires :

- **50 %** : probabilité issue du modèle supervisé ;
- **30 %** : signal issu d’Isolation Forest ;
- **20 %** : historique du client.

Les clients sont ensuite classés selon quatre niveaux de priorité :

- **Faible**
- **Modéré**
- **Élevé**
- **Critique**

Ce score permet de faciliter la priorisation des contrôles terrain.

---

## Structure du repository

```text
PFE-SRM-RSK/
│
├── Modelisation_ML_ameliore.ipynb
├── Preparation_Analyse_Donnees.ipynb
│
├── clusters_pca_powerbi.csv
├── importance_variables_powerbi.csv
├── metriques_modele_powerbi.csv
├── predictions_test_powerbi.csv
│
├── artefacts_modele/
│
├── README.md
└── .gitignore

