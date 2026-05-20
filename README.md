# Customer Segmentation — K-Means vs DBSCAN

A comparative study of **K-Means** and **DBSCAN** clustering algorithms on the [Marketing Campaign](https://www.kaggle.com/datasets/imakash3011/customer-personality-analysis) dataset to identify distinct customer segments.

---

## Project Overview

This project walks through the full data-science pipeline:

1. **Exploratory Data Analysis (EDA)** — cleaning, imputation, feature engineering, outlier removal, and standardisation.  
2. **K-Means Clustering** — elbow method, silhouette analysis, and Davies-Bouldin evaluation to find the optimal number of clusters.  
3. **DBSCAN Clustering** — k-distance graphs for `eps` tuning, runs on both the full feature space and PCA-reduced data.  
4. **Benchmark Comparison** — side-by-side evaluation of both algorithms using Silhouette Score, Davies-Bouldin Index, and Calinski-Harabasz Index.

### Key Finding

> K-Means (k = 5) significantly outperformed DBSCAN on this dataset.  
> DBSCAN consistently collapsed the data into a single dense cluster regardless of hyper-parameter tuning, while K-Means produced five well-separated customer segments.

---

## Repository Structure

```
ds_proj/
├── marketing_campaign.csv              # Raw dataset (tab-separated)
├── eda.ipynb                           # EDA & preprocessing notebook
├── dataset_cleaned.csv                 # Cleaned & scaled dataset
├── kmean.ipynb                         # K-Means clustering analysis
├── dbs.ipynb                           # DBSCAN clustering analysis
├── compare.ipynb                       # Head-to-head benchmark
├── analysis_process_documentation.txt  # Detailed process documentation
├── analysis_process_documentation.pdf  # PDF version of documentation
├── plot.png                            # Supporting plot
├── venv/                               # Python virtual environment (gitignored)
└── README.md
```

---

## EDA & Preprocessing Summary

| Step | Details |
|------|---------|
| **Missing values** | 24 missing `Income` values imputed via `KNNImputer(n_neighbors=5)` |
| **Feature engineering** | `Age`, `Loyalty_Time`, `Total_Spend`, spending share features, purchase channel shares, `Total_Promos_Accepted` |
| **Encoding** | `Education` → ordinal (1–4), `Marital_Status` → binary (0/1) |
| **Outlier removal** | `Age ≥ 85` and `Income ≥ 200 000` removed |
| **Scaling** | `StandardScaler` applied to all 23 final features |
| **Final shape** | 2 235 rows × 23 columns |

---

## Clustering Results

| Metric | K-Means (k=5) | PCA + DBSCAN (eps=1.2, min_pts=3) |
|--------|:-:|:-:|
| Valid Clusters | 5 | 2 |
| Noise Points | 0 | 14 |
| Silhouette Score ↑ | 0.1243 | 0.2578 |
| Davies-Bouldin ↓ | **1.9146** | 2.4026 |
| Calinski-Harabasz ↑ | **274.92** | 10.10 |

> **Note:** DBSCAN's higher Silhouette Score is misleading — it results from nearly all points being assigned to a single cluster.

---

## How to Run

```bash
# 1. Clone the repository
git clone https://github.com/<your-username>/ds_proj.git
cd ds_proj

# 2. Create and activate a virtual environment
python3 -m venv venv
source venv/bin/activate

# 3. Install dependencies
pip install numpy pandas matplotlib seaborn scikit-learn yellowbrick plotly

# 4. Launch Jupyter
jupyter notebook
```

Open the notebooks in order: `eda.ipynb` → `kmean.ipynb` → `dbs.ipynb` → `compare.ipynb`.

---

## Technologies Used

- Python 3.12
- NumPy · Pandas · Matplotlib · Seaborn
- Scikit-learn (KMeans, DBSCAN, PCA, KNNImputer, StandardScaler, metrics)
- YellowBrick (Silhouette Visualizer)
- Plotly Express (3D scatter visualisation)

---

## License

This project is for educational purposes.
