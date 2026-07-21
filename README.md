# (Skripsi) Japanese Lemmas Clustering & Translation Analysis

This project is part of the thesis research to organize and group Japanese vocabulary (lemmas) based on the frequency of use and linguistic characteristics using the "K-Means Clustering" algorithm, and translate it into Indonesian using an AI-based model.

# Project Workflow

1. Machine Translation:
   * Translate 15,000 Japanese lemmas from `japanese_lemmas.csv` using the "Neural Machine Translation" models (`Helsinki-NLP/opus-mt-ja-en` and `Helsinki-NLP/opus-mt-en-id`) via the "pipeline/chain-translation" technique (JA -> EN -> ID).
   * The computing process is accelerated using GPU acceleration (CUDA).

2. Feature Engineering & Preprocessing:
   * Additional feature extraction from Japanese text: word character length (`lemma_length`) and Kanji usage ratio (`kanji_ratio`) based on Regex.
   * Standardize features using `StandardScaler` before the clustering process.

3. K-Means Clustering:
   * Determining the optimal number of groups through the "Elbow Method" or Inertia.
   * Grouping vocabulary into 4 main clusters based on a combination of features: Rank, Frequency, Lemma Length, and Kanji Ratio.

# Cluster Characteristics

The final clustering results in `clustered_japanese_lemmas.csv` map vocabulary into 4 teaching curriculum segmentations:
*   Cluster 3 (Core Grammar / N5): Contains 10 main particles (の, に, は, etc.) with super high frequency and no Kanji components.
*   Cluster 0 (Basic Vocabulary / N5-N4): Daily functional verbs/adjectives (ます, ない, いる) with high frequency and low Kanji ratio.
*   Cluster 1 (Compound Sentence Patterns / N4-N3): Grammatical patterns and long-character connecting words (という, できる, として).
*   Cluster 2 (Advanced Kanji Vocabulary / N2-N1): Abstract nouns and formal terms dominated by 95% Kanji characters (核兵器, 来年度).

# Model Evaluation

Clustering accuracy and validation are measured using two main metrics:
*   Silhouette Score: `0.387` .
*   Davies-Bouldin Index: `0.728` .

#  Tech Stack & Dependencies

*   Language: Python 3.12+
*   Libraries: `pandas`, `torch` (CUDA Enabled), `transformers` (Helsinki-NLP Models), `tqdm`, `scikit-learn`, `matplotlib`, `seaborn`
*   Hardware: Tested on NVIDIA GeForce RTX 5050 Laptop GPU
