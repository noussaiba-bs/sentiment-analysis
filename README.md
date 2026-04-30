# Sentiment analysis on product reviews

**Text classification** project: predict sentiment (**positive**, **neutral**, **negative**) from review text, using a classic **NLP + scikit-learn** pipeline (TF-IDF, multiple models, performance comparison).


## Results

| Model | Accuracy | Precision | Recall | F1-Score | Training Time |
|-------|----------|-----------|--------|----------|----------------|
| **Logistic Regression** | 92.3% | 0.92 | 0.92 | 0.92 | 2.5s |
| **Random Forest** | 89.7% | 0.90 | 0.89 | 0.89 | 45.2s |
| **Naive Bayes** | 88.1% | 0.88 | 0.88 | 0.88 | 0.8s |

**Best model**: Logistic Regression with **92.3% accuracy**

---

## Objective

Create an automatic sentiment analysis system capable of classifying customer reviews into three categories:

- **Positive** (Score 4-5) - Favorable reviews
- **Neutral** (Score 3) - Mixed reviews
- **Negative** (Score 1-2) - Unfavorable reviews

This project demonstrates the practical application of **Natural Language Processing (NLP)** and **Machine Learning** to solve a real-world customer opinion analysis problem.

---

## Dataset

**Amazon Fine Food Reviews**
- Source: [Kaggle - Amazon Fine Food Reviews](https://www.kaggle.com/datasets/snap/amazon-fine-food-reviews)
- Size: ~500,000+ customer reviews
- Period: 1999-2012
- Content: Textual reviews with ratings from 1 to 5 stars

**Dataset characteristics used:**
- English textual reviews
- Rating scores (1-5 stars)
- Cleaned and preprocessed data

---

## Methodology

### **Data Exploration**
- Analysis of sentiment distribution
- Text length statistics
- Identification of most frequent words
- Visualization with word clouds

### **Text Preprocessing**
Cleaning techniques applied:
- Lowercase conversion
- Removal of URLs and mentions
- Removal of punctuation and numbers
- Stop words filtering
- Lemmatization (reduction to root form)
- Tokenization

### **Feature Engineering**
- **TF-IDF Vectorization** (Term Frequency - Inverse Document Frequency)
  - 5,000 selected features
  - Unigrams and Bigrams (1-2 words)
  - Filtering of too rare or too frequent words

### **Models Implemented**

**Logistic Regression**
- Simple but effective linear classification
- L2 regularization to avoid overfitting
- **Best performance**: 92.3% accuracy

**Random Forest**
- Ensemble of 100 decision trees
- Robust but slower to train
- Performance: 89.7% accuracy

**Multinomial Naive Bayes**
- Based on Bayes' theorem
- **Very fast** (0.8s training time)
- Performance: 88.1% accuracy

### **Evaluation**
- Train/Test Split: 80/20
- Metrics: Accuracy, Precision, Recall, F1-Score
- Confusion matrices for each model
- Cross-validation

---


## Repository structure

```
├── data/                    # Data (see Data section)
├── images/                  # Generated graphs and word clouds
├── models/                  # tfidf_vectorizer.pkl, best_model.pkl, metadata.pkl
├── notebooks/
│   └── sentiment_analysis.ipynb
├── model_comparison.csv     # Summary metrics table (generated)
├── requirements.txt
└── README.md
```


## Installation

At the project root:

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

## Data

The notebook reads the file **`data/Reviews.csv`**.

- Common public dataset: [Amazon Fine Food Reviews on Kaggle](https://www.kaggle.com/datasets/snap/amazon-fine-food-reviews) (file named **`Reviews.csv`**).

Expected columns (minimum): **`Score`** (1–5) and **`Text`**.

## Running the notebook

Paths (`data/`, `images/`, `models/`) are **relative to the project root**. You must start Jupyter **from this root**:

```bash
cd path/to/sentiment-analysis
jupyter notebook notebooks/sentiment_analysis.ipynb
```

Or with JupyterLab:

```bash
jupyter lab notebooks/sentiment_analysis.ipynb
```

## Results produced (after full execution)

| Output | Description |
|--------|-------------|
| `data/reviews_cleaned.csv` | Data with cleaned text |
| `models/tfidf_vectorizer.pkl` | Trained vectorizer |
| `models/best_model.pkl` | Best classifier (according to notebook accuracy) |
| `models/metadata.pkl` | Metadata (model, metrics, date) |
| `model_comparison.csv` | Comparison of the 3 models |
| `images/*.png` | EDA, confusion matrices, comparison, word clouds |


## Limitations

- Sentiment inferred from **stars** (approximation; text may contradict the rating)
- Often **imbalanced** classes; weighted metrics are not always sufficient to judge the minority class
- **Sarcasm/Irony**: Difficulty detecting second-degree language
