# CSCE676 Project: Decoding Outliers In Cinema 

### 📖 1. Project Overview
The modern film industry relies on massive data to predict audience engagement, but these standard industry metrics create a feedback loop that highlights safe, repetitive blockbuster formulas (e.g., Action-Adventure, Romantic Comedies) while drowning out nuanced storytelling. Furthermore, gender representation is sometimes overlooked within certain genres in favor of financial gain. To look beyond the industry baseline, I implemented a two-step pipeline designed to isolate and analyze "Representation Outliers." First, the pipeline utilizes a Multivariate Isolation Forest to detect structural anomalies, which is the subset of films that successfully break standard representation boundaries. Second, it deploys Apriori Association Rule Mining exclusively on this isolated subset to uncover their hidden genre combinations.

### 👉 2. The Main Notebook
The main deliverable is **`main_notebook.ipynb`**.

### 🎯 3. Research Question
How do high-lift genre associations within representation outliers—isolated via a multivariate Isolation Forest—differ from those of the standard movie population?

### 🎥 4. Project Presentation Video
[**Click to Watch Project Video**](https://www.youtube.com/watch?v=ZuZuaeUwGB4)

### 📊 5. Data & Preprocessing
**Dataset Source:** [9000+ Movies : IMDb and Bechdel (Kaggle)](https://www.kaggle.com/datasets/nliabzd/movies-imdb-and-bechdel-information)
* **Size:** ~9,000+ Movies (1894 - 2024)
* **Key Features:** `Title`, `Year`, `IMDb Rating`, `Bechdel Score` (0-3), `Genre 1`, `Genre 2`, `Genre 3`  It contains data from **Bechdel Test API** (providing a 0-3 categorical representation baseline) and the raw **IMDb Database** (providing continuous metrics like runtime and ratings, plus genre tags). 

**Preprocessing Steps:**
* **Artifact Handling:** Aggressively cleaned IMDb's infamous `\N` string artifacts, enforcing numeric data types for continuous variables for Isolation Forest phase.
* **"No Imputation" Strategy:** Instead of using standard mean imputation for missing values (which would artificially pull anomalous movies toward the center and destroy the target signal), rows missing critical continuous data were strictly dropped.
* **Matrix Encoding:** Cleaned text arrays and deployed a `TransactionEncoder` to convert categorical genre tags into a sparse One-Hot Encoded matrix for the Apriori algorithm. 

### 🚀 6. How to Reproduce Your Work
This project was built and executed in **Google Colab**. 
1. Download or clone this repository and upload the entire folder directly to your Google Drive.
2. Open Google Colab, mount your Google Drive, and open the main_notebook.ipynb file from your uploaded folder.
3. Install all necessary dependencies by running the following command in a notebook cell: !pip install -r requirements.txt
4. Run the notebook cells sequentially from top to bottom.

### 🌱 7. Key Dependencies
The complete list is available in `requirements.txt`, but core packages include:
* `python` (3.12.13)
* `pandas` (v2.2.2) - For rigorous data filtration and matrix encoding
* `scikit-learn` (v1.6.1) - For the `IsolationForest` anomaly phase
* `mlxtend` (v0.23.4) - For `apriori` and `association_rules` pattern mining
* `seaborn` (v0.13.2) / `matplotlib` (v3.10.0) - For high-contrast structural visualization

### 🗂️ 8. Repository Structure
```text
├── README.md
├── requirements.txt
├── main_notebook.ipynb       
├── checkpoints/              
│   ├── checkpoint_1.ipynb    # Early exploratory data analysis (EDA)
│   └── checkpoint_2.ipynb    # Initial model testing and hyperparameter tuning
└──data/
    └── Bechdel_IMDB_Merge0524.csv
```

### ✨ 9. Results Summary

Standard industry formulas actively suppress complex representation. While standard blockbusters rely on mathematically safe, weak genre correlations (peaking at a **2.53x Lift**), true "Representation Outliers" are driven by highly concentrated, complex genre combinations. Specifically, the outlier trifecta of **(Drama + Biography) → History** achieves an explosive **6.16x Correlation Strength**. 

For studios and data analysts, this proves that capturing untapped, high-value audiences requires intentionally abandoning the safety of the industry average to target tightly bound, niche narratives.
