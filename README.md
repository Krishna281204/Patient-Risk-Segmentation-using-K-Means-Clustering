# 🫀 Patient Risk Segmentation using K-Means Clustering

Unsupervised machine learning project applying K-Means clustering to identify natural groupings in patient data, validated on a synthetic dataset and applied to a real-world heart disease dataset.

---

## 📌 Problem Statement

Can we group patients into meaningful segments based on clinical features like age, cholesterol, blood pressure, and heart rate — **without using labeled diagnoses?**

This project explores unsupervised clustering as a tool for patient risk segmentation, using multiple evaluation metrics to determine the optimal number of clusters and assess cluster quality.

---

## 📂 Dataset

| | Details |
|---|---|
| **Dataset 1** | Synthetic — 200 samples, 3 centers, generated via `make_blobs` (used for algorithm validation) |
| **Dataset 2** | [Heart Disease Dataset (Kaggle)](https://www.kaggle.com/datasets/fedesoriano/heart-failure-prediction) — 918 real patient records |

**Features used from heart dataset:** `Age`, `RestingBP`, `Cholesterol`, `MaxHR`, `Oldpeak`, `FastingBS`, `HeartDisease`

---

## ⚙️ Workflow

```
Raw Data → Preprocessing → K-Means Clustering → Optimal K Selection → Evaluation → Visualization
```

1. **Data Preprocessing** — Selected numeric features, handled missing values via mean imputation, normalized using `StandardScaler`
2. **K-Means Clustering** — Random initialization, `n_init=10` restarts, `max_iter=300`
3. **Optimal K Selection** — Elbow Method (SSE/Inertia) + Silhouette Coefficient, evaluated across K = 2 to 10
4. **Model Evaluation** — Davies-Bouldin Score and Silhouette Coefficient on final clusters
5. **Visualization** — Cluster boundaries and centroids plotted using Matplotlib and Seaborn

---

## 📊 Results

### Dataset 1 — Synthetic Data

| Metric | Value |
|---|---|
| Optimal K (Silhouette) | **3** |
| Max Silhouette Coefficient | **0.5979** |
| Davies-Bouldin Score | **0.5713** |
| SSE (Inertia) | 72.56 |
| Iterations to Converge | 9 |

> Silhouette score of ~0.60 and DB score of 0.57 indicate **well-separated, compact clusters** — expected on synthetic data with clearly defined centers.

---

### Dataset 2 — Heart Disease Dataset

| Metric | Value |
|---|---|
| Optimal K (Silhouette) | **4** |
| Max Silhouette Coefficient | **0.2455** |
| Davies-Bouldin Score | **1.6947** |
| SSE (Inertia) | 4201.49 |
| Iterations to Converge | 11 |

> The lower Silhouette score (0.24) and higher DB score (1.69) reflect the **overlapping nature of real clinical data** — patient risk groups don't separate as cleanly as synthetic clusters. This is expected and consistent with findings in medical clustering literature.

---

## 🔍 Key Observations

- **Optimal K differed between datasets** (3 for synthetic, 4 for heart data), demonstrating that the Elbow Method and Silhouette Coefficient can disagree — using both together leads to a more reliable decision
- **Cluster 2** (low `FastingBS`, higher `MaxHR`, negative `HeartDisease` loading) likely represents **younger, lower-risk patients**
- **Cluster 1** (higher `Oldpeak`, positive `HeartDisease` loading) likely captures **higher-risk patients** — consistent with `Oldpeak` being a known cardiac stress indicator
- Preprocessing with `StandardScaler` was critical — without normalization, features like `Cholesterol` (range: 0–600) would dominate over `FastingBS` (range: 0–1), skewing cluster assignments

---

## 🛠️ Tech Stack

![Python](https://img.shields.io/badge/Python-3.x-blue)
![Scikit-learn](https://img.shields.io/badge/Scikit--learn-ML-orange)
![Pandas](https://img.shields.io/badge/Pandas-Data-green)
![Colab](https://img.shields.io/badge/Google-Colab-yellow)

- **Language:** Python 3
- **Libraries:** NumPy, Pandas, Scikit-learn, Matplotlib, Seaborn
- **Environment:** Google Colab

---

## 📁 Repository Structure

```
├── kmeans_heart_segmentation.ipynb   # Full notebook with code, outputs, and visualizations
├── heart.csv                         # Heart disease dataset (or link to source below)
└── README.md
```

> **Note:** If `heart.csv` is not included, download it from [Kaggle](https://www.kaggle.com/datasets/fedesoriano/heart-failure-prediction) and upload it to your Colab session before running.

---

## 🚀 How to Run

1. Clone the repo or open the notebook directly in Google Colab
2. Upload `heart.csv` when prompted (or update the file path in the notebook)
3. Run all cells in order (`Runtime → Run all`)

---

## 📚 Concepts Covered

`K-Means Clustering` &nbsp; `Unsupervised Learning` &nbsp; `Elbow Method` &nbsp; `Silhouette Analysis` &nbsp; `Davies-Bouldin Score` &nbsp; `Feature Scaling` &nbsp; `EDA` &nbsp; `Data Preprocessing`
