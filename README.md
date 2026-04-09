# Analyse de sentiments sur des avis produits

Projet de **classification de texte** : prédire le sentiment (**positif**, **neutre**, **négatif**) à partir du texte d’un avis, avec un pipeline classique **NLP + scikit-learn** (TF-IDF, plusieurs modèles, comparaison des performances).


## Résultats

| Modèle | Accuracy | Precision | Recall | F1-Score | Temps d'entraînement |
|--------|----------|-----------|--------|----------|----------------------|
| **Logistic Regression** | 92.3% | 0.92 | 0.92 | 0.92 | 2.5s |
| **Random Forest** | 89.7% | 0.90 | 0.89 | 0.89 | 45.2s |
| **Naive Bayes** | 88.1% | 0.88 | 0.88 | 0.88 | 0.8s |

**Meilleur modèle** : Logistic Regression avec **92.3% d'accuracy** 

---

## Objectif

Créer un système automatique d'analyse de sentiments capable de classifier des avis clients en trois catégories :

-  **Positif** (Score 4-5) - Avis favorables
-  **Neutre** (Score 3) - Avis mitigés
-  **Négatif** (Score 1-2) - Avis défavorables

Ce projet démontre l'application pratique du **Natural Language Processing (NLP)** et du **Machine Learning** pour résoudre un problème réel d'analyse d'opinions clients.

---

##  Dataset

**Amazon Fine Food Reviews**
-  Source : [Kaggle - Amazon Fine Food Reviews](https://www.kaggle.com/datasets/snap/amazon-fine-food-reviews)
-  Taille : ~500,000+ avis clients
-  Période : 1999-2012
-  Contenu : Avis textuels avec scores de 1 à 5 étoiles

**Caractéristiques du dataset utilisé :**
- Avis textuels en anglais
- Scores de notation (1-5 étoiles)
- Données nettoyées et prétraitées

---

## Méthodologie

### **Exploration des Données**
- Analyse de la distribution des sentiments
- Statistiques sur la longueur des textes
- Identification des mots les plus fréquents
- Visualisation avec word clouds

### **Preprocessing du Texte**
Techniques de nettoyage appliquées :
-  Conversion en minuscules
-  Suppression des URLs et mentions
-  Suppression de la ponctuation et des chiffres
-  Filtrage des stop words (mots vides)
-  Lemmatization (réduction au radical)
-  Tokenization

### **Feature Engineering**
- **TF-IDF Vectorization** (Term Frequency - Inverse Document Frequency)
  - 5,000 features sélectionnées
  - Unigrams et Bigrams (1-2 mots)
  - Filtrage des mots trop rares ou trop fréquents

### **Modèles Implémentés**

**Logistic Regression** 
- Classification linéaire simple mais efficace
- Régularisation L2 pour éviter l'overfitting
- **Meilleure performance** : 92.3% d'accuracy

**Random Forest** 
- Ensemble de 100 arbres de décision
- Robuste mais plus lent à entraîner
- Performance : 89.7% d'accuracy

**Multinomial Naive Bayes** 
- Basé sur le théorème de Bayes
- **Très rapide** (0.8s d'entraînement)
- Performance : 88.1% d'accuracy

### **Évaluation**
- Split Train/Test : 80/20
- Métriques : Accuracy, Precision, Recall, F1-Score
- Matrices de confusion pour chaque modèle
- Validation croisée

---


## Structure du dépôt

```
├── data/                    # Données (voir section Données)
├── images/                  # Graphiques et nuages de mots générés
├── models/                  # tfidf_vectorizer.pkl, best_model.pkl, metadata.pkl
├── notebooks/
│   └── sentiment_analysis.ipynb
├── model_comparison.csv     # Tableau récap des métriques (généré)
├── requirements.txt
└── README.md
```


## Installation

À la racine du projet :

```bash
python -m venv venv
```

**Windows (PowerShell)**

```powershell
.\venv\Scripts\Activate.ps1
pip install -r requirements.txt
```

**Linux / macOS**

```bash
source venv/bin/activate
pip install -r requirements.txt
```

## Données

Le notebook lit le fichier **`data/Reviews.csv`**.

- Jeu public courant : [Amazon Fine Food Reviews sur Kaggle](https://www.kaggle.com/datasets/snap/amazon-fine-food-reviews) (fichier nommé **`Reviews.csv`**).


Colonnes attendues (au minimum) : **`Score`** (1–5) et **`Text`**.

## Lancer le notebook

Les chemins (`data/`, `images/`, `models/`) sont **relatifs à la racine du projet**. Il faut donc démarrer Jupyter **depuis cette racine** :

```bash
cd chemin/vers/sentiment-analysis
jupyter notebook notebooks/sentiment_analysis.ipynb
```

Ou avec JupyterLab :

```bash
jupyter lab notebooks/sentiment_analysis.ipynb
```

## Résultats produits (après exécution complète)

| Sortie | Description |
|--------|-------------|
| `data/reviews_cleaned.csv` | Données avec texte nettoyé |
| `models/tfidf_vectorizer.pkl` | Vectoriseur entraîné |
| `models/best_model.pkl` | Meilleur classifieur (selon accuracy du notebook) |
| `models/metadata.pkl` | Métadonnées (modèle, métriques, date) |
| `model_comparison.csv` | Comparaison des 3 modèles |
| `images/*.png` | EDA, matrices de confusion, comparaison, word clouds |


## Limites 

- Sentiment déduit des **étoiles** (approximation ; le texte peut contredire la note).
- Classes souvent **déséquilibrées** ; les métriques *weighted* ne suffisent pas toujours à juger la classe minoritaire.
- **Sarcasme/Ironie** : Difficulté à détecter le second degré


