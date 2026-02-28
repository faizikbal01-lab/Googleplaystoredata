# Google Play Store App Analysis & Market Insights (EDA)

## Project Overview

The Google Play Store is one of the largest digital marketplaces in the world, hosting millions of applications across dozens of categories. Understanding what drives app ratings, installs, and user engagement is critical for developers, product managers, and market strategists. This project presents a focused **Exploratory Data Analysis (EDA)** of Google Play Store app records, covering app ratings, size distributions, install counts, content classifications, and review patterns across Free and Paid app types.

As a **Business and Data Analyst**, the objective was to clean and interrogate raw Play Store metadata to surface trends that can inform competitive strategy, app positioning, and market targeting decisions.

---

## Business & Product Strategy Objectives

The analysis seeks to provide data-backed answers to the following critical questions:

1. **Rating Benchmarks:** What is the average app rating across the entire Play Store, and what does the distribution look like across categories?
2. **App Size Patterns:** How are app file sizes distributed — and are heavier apps penalized or rewarded in terms of user engagement?
3. **Market Segmentation:** Which app categories dominate the Play Store, and how diverse is the category landscape?
4. **Monetization Split:** What is the ratio of Free vs. Paid apps, and how does monetization type affect average review volume?
5. **Top Performers:** Which apps lead in total installs, and what attributes do the most-installed apps share?
6. **Data Quality & Anomalies:** Where do inconsistencies (e.g., malformed category entries, mixed-format fields) appear in the dataset, and how should they be resolved?

---

## Dataset Description

The analysis is based on the publicly available Google Play Store dataset (`googleplaystore.csv`) with records across the following key attributes:

| Feature | Description |
| --- | --- |
| `App` | Name of the application. |
| `Category` | App category on the Play Store (e.g., GAME, SOCIAL, TOOLS). |
| `Rating` | Average user rating (out of 5). |
| `Reviews` | Number of user reviews (raw string format — requires cleaning). |
| `Size` | App size (stored as strings: e.g., "19M", "512k", "Varies with device"). |
| `Installs` | Number of installs (stored as strings: e.g., "10,000+"). |
| `Type` | Monetization type: Free or Paid. |
| `Price` | App price in USD (for Paid apps). |
| `Content Rating` | Target audience classification (e.g., Everyone, Teen, Mature 17+). |
| `Genres` | Sub-genre tags for the app. |
| `Last Updated` | Date the app was last updated on the store. |
| `Current Ver` | Current version of the app. |
| `Android Ver` | Minimum Android version required. |

---

## Methodology & Technical Stack

### Technologies Used

- **Python:** Core language for all data processing and analysis.
- **Pandas:** Data loading, cleaning, filtering, aggregation, and anomaly detection.
- **NumPy:** Numerical operations and handling of missing/invalid values during size conversion.
- **Matplotlib:** Histogram visualization for app size distribution.

### Analytical Workflow

1. **Data Loading:** Loaded `googleplaystore.csv` using Pandas and performed initial inspection of shape, columns, and data types.
2. **Rating Analysis:** Computed the mean rating across all apps to establish a baseline benchmark for the Play Store.
3. **Category Enumeration:** Extracted all unique app categories to map the full breadth of the Play Store's taxonomy.
4. **Size Cleaning & Visualization:** Built a custom `clean_size()` function to parse mixed-format size strings (`M` for megabytes, `k` for kilobytes, `"Varies with device"` mapped to `NaN`). Plotted the cleaned size distribution as a histogram to identify the most common app size ranges.
5. **App Type Distribution:** Used `value_counts()` on the `Type` column to quantify the Free-vs-Paid split across all listed apps.
6. **Content Rating Mode:** Identified the most frequent content rating classification to understand the primary target audience of Play Store apps.
7. **Anomaly Detection:** Isolated rows where `Category == '1.9'` — a known data quality issue in this dataset — to flag corrupted or misaligned records for exclusion.
8. **Install Cleaning & Top Apps:** Developed a `clean_installs()` function to strip `+` and `,` characters and convert install counts to integers. Ranked apps by install count to surface the top 5 most-installed applications.
9. **Rating-Based Filtering:** Filtered the full dataset to retain only apps with `Rating >= 4.0`, creating a high-quality app subset for further analysis.
10. **Review Analysis by Type:** Built a `clean_reviews()` function to handle `M`-suffixed values (e.g., `"1.5M"`). Computed mean review counts grouped by `Type` (Free vs. Paid) to compare engagement levels across monetization models.

---

## Key Insights (Executive Summary)

- **The Play Store spans 33+ distinct app categories**, from ART_AND_DESIGN to WEATHER, reflecting the platform's enormous breadth of content and competitive segments.
- **Free apps dominate the marketplace** by a significant margin, with Paid apps representing a small fraction of total listings — highlighting how freemium and ad-supported models are the norm, not the exception.
- **"Everyone" is the most common Content Rating**, confirming that the majority of apps on the Play Store are designed for a general, all-ages audience — a key consideration for ad-targeting and family-safe filtering.
- **App sizes are right-skewed** — most apps are relatively lightweight (under 20MB), while a long tail of heavy applications (games, creative tools) extends well beyond 100MB. "Varies with device" entries require careful handling and represent a non-trivial portion of the catalogue.
- **Free apps attract far higher average review volumes than Paid apps**, confirming that lower barriers to entry drive significantly greater user engagement and feedback loops for Free applications.
- **Data quality issues are present in the raw dataset** — including a row where `Category` contains the numeric value `'1.9'`, indicating a row misalignment in the original CSV that must be excluded before analysis.
- **Installs data required extensive cleaning** — raw values were stored as formatted strings (e.g., `"10,000+"`) and a special case where `"Free"` appeared in the Installs column had to be handled explicitly, underscoring the importance of robust data cleaning pipelines before any analysis.
- **High-rated apps (≥ 4.0) form a strong subset** of the catalogue, providing a clean pool for benchmarking quality standards, feature patterns, and category-level performance comparisons.

---

## How to Run

1. **Clone the Repository:**
   ```bash
   git clone <your-repo-url>
   ```

2. **Install Dependencies:**
   ```bash
   pip install pandas numpy matplotlib
   ```

3. **Add the Dataset:** Place `googleplaystore.csv` in the root project directory (same level as the notebook).

4. **Open the Notebook:** Run `googleplaystoredaTA.ipynb` cell by cell to reproduce the full cleaning pipeline, analysis, and visualizations.

---

## Author

**[Mohd Faiz]**

- **Role:** Business and Data Analyst
- **GitHub:** [https://github.com/faizikbal01-lab](https://github.com/your-github-handle)

---

*Disclaimer: This analysis is based on a publicly available Google Play Store dataset and is intended for educational and research purposes only. App market conditions and store listings change frequently; findings should not be used as the sole basis for product or investment decisions.*

