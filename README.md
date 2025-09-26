## Résumer Projet Prédiction du Churn

### Objectif du projet
Le churn bancaire est le fait qu'un client ou détenteur de compte dans une banque cloture sont compte après un certain temps de contrat.
L’objectif de ce projet est de prédire le churn des clients afin d’anticiper leur départ et de mettre en place des actions marketing ciblées pour les fidéliser. 
La prédiction du churn permettra d’optimiser les campagnes et de maximiser la rétention client.

---
### Données utilisées

Dataset : <a href ="https://raw.githubusercontent.com/selva86/datasets/refs/heads/master/Churn_Modelling_m.csv">Churn_Modelling</a>

  Prétraitement :

- Gestion des valeurs manquantes
- Encodage des variables catégorielles
- Sandardisation
---
### Modélisation

##### Résumer et comparaison des modèles utilisés

| Modèle | Accuracy | f1 (Classe Non Churner) | f1 (Classe Curners) | 
|--------|:--------:|:-------------:|:-------------:|
| **Régression logistique** | 0.73     | 0.81          | 0.50          |
| **Régression logistique avec RFE** | 0.73     | 0.81          | 0.51          |
| **Fôret aléatoire** | 0.86     | 0.91          | 0.60          |
| **Fôret aléatoire avec RFE** | 0.82     | 0.89          | 0.51          |

Comme on peut le voir le modèle 3 de fôret aléatoire est le best : 
- Bon compromis Accuracy & f1 Score 
- Meilleur prédiction sur la classe minoritaire (Churner)

Modèle final : Random Forest Classifier (intégré dans un pipeline complet)

- Hyperparamètres optimisés :   `n_estimators=100` (GridSearchCV)
- Traitement du déséquilibre de classe : Méthode de sur-échantillonage (**Oversamplinng**)
- Métrics d'évaluation : `F1_Score` pour mieux refléter la performance sur la classe minoritaire “churners”
---
### Évaluation

Performance globale :

- Accuracy : 86%
- F1-score par classe :
  - Clients qui restent : 92%
  - Clients churners : 62%

> Note : La détection des churners reste plus difficile à cause du déséquilibre de classe (même après réechantillonage), 
mais le modèle identifie correctement une majorité de churners tout en minimisant les faux positifs.

---

### Interprétation et insights

Features les plus importantes (Top 5) :

`Age, Balance, EstimatedSalary, NumOfProducts, CréditScore, Tenure`



- Les clients qui on,t entre 40 ent 50 ans avec un solde médian de 100.000 Euro ont un risque plus élevé de churn.

- Les clients avec plusieurs produits bancaires ou une longue ancienneté sont moins susceptibles de churner.


<img width="556" height="545" alt="output" src="https://github.com/user-attachments/assets/a0f6e76e-e444-4304-8532-d71f28edbcdd" />

---
### Recommandations

Actions sur les clients churners : campagnes marketing ciblées, offres personnalisées, suivi personnalisé.

Améliorations possibles du modèle :

- Essayer des modèles plus puissants (XGBoost, LightGBM)
- SMOTE pour mieux traiter la classe minoritaire
