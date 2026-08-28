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

## Tableau de bord Power BI

Les résultats analytiques sont intégrés dans un tableau de bord décisionnel développé sous **Microsoft Power BI**.

Le dashboard permet notamment de suivre :

- la consommation d’eau ;
- la consommation d’électricité ;
- le montant facturé ;
- le nombre de clients ;
- le taux de comportements suspects ;
- les anomalies détectées ;
- le score de risque moyen ;
- les facteurs clés du risque ;
- les niveaux de priorité ;
- les profils clients ;
- la répartition géographique ;
- les performances des modèles ;
- les clients à contrôler en priorité.

L’objectif est de transformer les résultats des modèles en informations directement exploitables par les responsables métier.

---

## Aide à la décision

La solution vise à fournir un outil permettant de :

1. détecter les situations inhabituelles ;
2. estimer la probabilité d’un comportement suspect ;
3. expliquer les facteurs ayant conduit à l’alerte ;
4. attribuer un score de risque ;
5. classer les clients selon leur priorité ;
6. orienter les contrôles terrain.

---

## Perspectives

Plusieurs améliorations peuvent être envisagées :

- validation sur des données réelles ;
- intégration de compteurs intelligents ;
- analyse à une granularité temporelle plus fine ;
- utilisation de modèles séquentiels tels que LSTM ou Temporal Fusion Transformer ;
- automatisation des flux de données ;
- monitoring des modèles ;
- détection de dérive ;
- réentraînement périodique ;
- intégration complète avec Power BI Service ;
- réintégration des résultats des contrôles terrain dans la chaîne d’apprentissage.

---

## Auteur

**Echchihaby Majda**  
Projet de Fin d’Études  
Cycle Ingénieur

---

## Contexte académique

Projet réalisé dans le cadre d’un **Projet de Fin d’Études en Intelligence Artificielle et Data Science**.

---

## Contexte métier

**Société Régionale Multiservices Rabat–Salé–Kénitra (SRM-RSK)**

Le projet porte sur l’analyse intelligente de la consommation d’eau et d’électricité et sur la détection de comportements nécessitant une attention particulière.

---

## Avertissement

Ce repository est publié à des fins académiques et de démonstration.

Les données utilisées dans le mémoire sont synthétiques et réalistes afin de respecter les contraintes de confidentialité.

Les prédictions, anomalies et scores de risque produits par les modèles constituent des **indicateurs d’aide à la décision**.

Une anomalie, une alerte ou un niveau de risque élevé ne constitue pas une preuve de fraude. Toute situation signalée doit être confirmée par une analyse métier ou un contrôle terrain.
