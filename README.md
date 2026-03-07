# 📱 Google Play Store App Analysis — Market Insights (EDA)

A data analyst's deep-dive into the Google Play Store ecosystem — cleaning messy real-world data and extracting market insights on app ratings, installs, categories, pricing, and content to help developers and product teams make smarter publishing decisions.

---

## 📊 Key Insights at a Glance

- **Mean app rating** across the store computed and benchmarked
- **Top 5 most-installed apps** identified after cleaning raw install strings
- **Free vs. Paid** app distribution and average review comparison
- **Anomaly detected** — a rogue row with `Category = '1.9'` flagged and isolated
- **App size** normalized from mixed `M`/`k` string formats to bytes for analysis

---

## 🔍 What's Inside

- **Data Cleaning** — Size (`M`/`k` → bytes), Installs (`+`,`,` stripped), Reviews (`M` suffix handled), anomaly row isolation
- **Descriptive Stats** — Mean rating, mode of content rating, unique categories
- **Market Segmentation** — Free vs. Paid breakdown, top apps by installs
- **Filtering** — High-quality apps (Rating ≥ 4.0) isolated for further analysis
- **Visualizations** — App size distribution histogram

---

## 🗂️ Project Structure

```
Google_Play_Store_Analysis/
│
├── google_play_analysis.ipynb    # Main notebook (cleaning + EDA)
├── googleplaystore.csv           # Dataset (place in same directory)
└── README.md
```

---

## ⚙️ Requirements

- Python 3.8+
- Jupyter Notebook or Google Colab

---

## 🚀 Getting Started

**1. Clone the repository**
```bash
git clone https://github.com/your-username/google-play-store-analysis.git
cd google-play-store-analysis
```

**2. Install dependencies**
```bash
pip install pandas numpy matplotlib jupyter
```

> Or install in one command using the requirements file (if provided):
> ```bash
> pip install -r requirements.txt
> ```

**3. Add the dataset**

Place `googleplaystore.csv` in the root project folder (same level as the notebook).

> 📥 Dataset source: [Kaggle - Google Play Store Apps](https://www.kaggle.com/datasets/lava18/google-play-store-apps)

---

## 📌 Recommendations for Improvement

- [ ] Add a `requirements.txt` — currently dependencies must be installed manually
- [ ] Add more visualizations — category-wise rating distributions, top categories by installs, free vs. paid rating comparison
- [ ] Drop or flag the `Category = '1.9'` anomaly row at the top of the notebook so all downstream analysis is clean
- [ ] Add a correlation heatmap between `Rating`, `Reviews`, `Size`, and `Installs`
- [ ] Perform sentiment analysis on the companion `googleplaystore_user_reviews.csv` dataset for richer insight
- [ ] Segment analysis by `Content Rating` (Everyone, Teen, Mature) to find audience-specific trends
- [ ] Export cleaned DataFrame to `googleplaystore_cleaned.csv` so others don't have to re-run cleaning steps

---


## Author

**[Mohd Faiz]**

- **Role:** Business and Data Analyst
- **GitHub:** [https://github.com/faizikbal01-lab](https://github.com/your-github-handle)

---

*Disclaimer: This analysis is based on a publicly available Google Play Store dataset and is intended for educational and research purposes only. App market conditions and store listings change frequently; findings should not be used as the sole basis for product or investment decisions.*

