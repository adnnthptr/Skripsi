# Skripsi Clustering Bahasa Jepang (Japanese Lemmas Clustering & Translation Analysis)

Proyek ini merupakan bagian dari riset tesis untuk mengorganisasi dan mengelompokkan kosakata (lemma) bahasa Jepang berdasarkan tingkat frekuensi penggunaan dan karakteristik linguistiknya menggunakan algoritma "K-Means Clustering", serta menerjemahkannya ke bahasa Indonesia menggunakan model berbasis AI.

# Alur Kerja Proyek

1. Penerjemahan Otomatis (Machine Translation):
   * Menerjemahkan 15.000 lemma bahasa Jepang dari `japanese_lemmas.csv` menggunakan model "Neural Machine Translation" (`Helsinki-NLP/opus-mt-ja-en` dan `Helsinki-NLP/opus-mt-en-id`) melalui teknik "pipeline/chain-translation" (JA -> EN -> ID).
   * Proses komputasi dipercepat menggunakan akselerasi GPU (CUDA).

2. Feature Engineering & Preprocessing:
   * Ekstraksi fitur tambahan dari teks Jepang: panjang karakter kata (`lemma_length`) dan rasio penggunaan huruf Kanji (`kanji_ratio`) berbasis Regex.
   * Standardisasi fitur menggunakan `StandardScaler` sebelum proses clustering.

3. K-Means Clustering:
   * Menentukan jumlah kelompok optimal melalui "Metode Elbow" atau Inertia.
   * Mengelompokkan kosakata ke dalam "4 cluster" utama berdasarkan kombinasi fitur: "Rank, Frequency, Lemma Length, dan "Kanji Ratio".

# Karakteristik Cluster

Hasil akhir pengelompokan pada `clustered_japanese_lemmas.csv` memetakan kosakata ke dalam 4 segmentasi kurikulum pengajaran:
*   Cluster 3 (Grammar Inti / N5): Berisi 10 partikel utama (の, に, は, dll.) dengan frekuensi super tinggi dan tanpa komponen Kanji.
*   Cluster 0 (Kosakata Dasar / N5-N4): Kata kerja/sifat fungsional harian (ます, ない, いる) berfrekuensi tinggi dengan rasio Kanji rendah.
*   Cluster 1 (Pola Kalimat Majemuk / N4-N3): Pola tata bahasa dan kata penghubung yang berkarakter panjang (という, できる, として).
*   Cluster 2 (Kosakata Kanji Tingkat Lanjut / N2-N1): Kata benda abstrak dan istilah formal yang didominasi oleh 95% huruf Kanji (核兵器, 来年度).

# Evaluasi Model

Akurasi dan validasi pengelompokan diukur menggunakan dua metrik utama:
*   Silhouette Score: `0.387` (menunjukkan pemisahan struktur cluster yang cukup baik).
*   Davies-Bouldin Index: `0.728` (nilai di bawah 1.0 membuktikan tingkat kerapatan internal tiap cluster sangat tinggi).

#  Tech Stack & Dependensi

*   Language: Python 3.12+
*   Libraries: `pandas`, `torch` (CUDA Enabled), `transformers` (Helsinki-NLP Models), `tqdm`, `scikit-learn`, `matplotlib`, `seaborn`
*   Hardware: Diuji pada NVIDIA GeForce RTX 5050 Laptop GPU
