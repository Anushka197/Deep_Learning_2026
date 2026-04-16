# IT549: Deep Learning — Lab 2
## GloVe Pretrained Embeddings for Movie Text Prediction

> **Course:** IT549 – Deep Learning  
> **Name:** Anushka Prajapati  
> **Student ID:** 202301224  
> **Dataset:** [Movie Dataset (Kaggle)](https://www.kaggle.com/datasets/figolm10/movie-dataset)

---

## Objective

Use pretrained GloVe word embeddings on movie metadata text for two predictive tasks: regression to predict `voting_average` and multi-label classification to predict movie genres.

---

## Setup

```bash
pip install pandas numpy scikit-learn nltk torch wordcloud matplotlib seaborn tqdm
```

NLTK downloads: `punkt`, `punkt_tab`, `stopwords`, `wordnet`, `omw-1.4`

Place the GloVe `.txt` file and `movies.csv` in the project root before running the notebook.

---

## Task 1 — Data Preparation

**Columns used:** `overview`, `tagline`, `keywords`, `genre`, `voting_average`

**Text preprocessing pipeline:**
- Lowercase
- Remove URLs, punctuation, and digits
- Tokenize with NLTK `word_tokenize`
- Lemmatize with `WordNetLemmatizer`

**Split:** 70% train / 15% validation / 15% test (random seed = 42)

---

## Task 2 — GloVe Embedding Pipeline

- **Embedding:** 200-dimensional GloVe vectors
- **Document representation:** Average pooling of GloVe word vectors across all tokens present in the GloVe vocabulary
- Unknown tokens are skipped; documents with no known tokens receive a zero vector

---

## Task 3 — Rating Prediction (Regression)

**Inputs tested:** `overview`, `tagline`, `keywords` (one at a time)

**Baseline:** Global mean predictor

**Model architecture:**
```
Linear(200 → 128) → ReLU → Linear(128 → 64) → ReLU → Linear(64 → 1)
```

- **Loss:** MSELoss  
- **Optimizer:** Adam (lr=0.001)  
- **Epochs:** 50  
- **Metrics:** MSE, RMSE

---

## Task 4 — Genre Prediction (Multi-Label Classification)

**Inputs tested:** `overview`, `keywords` (one at a time)

**Model architecture:**
```
Linear(200 → 256) → ReLU → Linear(256 → 128) → ReLU → Linear(128 → 22)
```

- **Loss:** BCEWithLogitsLoss  
- **Optimizer:** Adam (lr=0.0005)  
- **Epochs:** 50  
- **Prediction threshold:** 0.3  
- **Metrics:** Micro-F1, Macro-F1, Hamming Loss, Jaccard Score

---

## Task 5 — Frequent Words per Genre

- Computed on preprocessed `overview` text per genre
- Top 10 most frequent content words per genre
- Bottom 10 least frequent words per genre (minimum frequency threshold: 3)
- Results exported to `task5_top_frequent_words.csv` and `task5_bottom_least_frequent_words.csv`

---

## Task 6 — Genre-Indicative Words Using TF-IDF

- **Vectorizer:** TF-IDF (max 10,000 features, unigrams, min_df=3)
- **Model:** Logistic Regression (one-vs-rest, per genre)
- Top 10 words by highest positive coefficient weight extracted per genre
- Results exported to `task6_genre_indicative_words.csv`
