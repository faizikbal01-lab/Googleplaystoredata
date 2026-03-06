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

## Recommendations for GitHub Upload

Before publishing this project to GitHub, the following improvements are recommended to maximise usability, reproducibility, and professional quality.

### 1. Data Quality & Cleaning

- **Remove or quarantine the `Category == '1.9'` row explicitly:** Rather than relying on users to remember this anomaly, add a dedicated cleaning step at the top of the notebook that drops misaligned rows and logs how many were removed. Document the known cause (CSV row-shift in the original file) in a comment.
- **Handle `"Free"` in the `Installs` column defensively:** The current `clean_installs()` function handles this as a special case. Extend it to catch any non-numeric string that may appear in numeric columns, and add a summary of how many rows were coerced or dropped during each cleaning step.
- **Standardise `"Varies with device"` handling across columns:** This placeholder appears in `Size`, `Android Ver`, and `Current Ver`. Ensure all three are mapped to `NaN` consistently, and document the proportion of records affected per column — it may be material for `Android Ver` analyses.
- **Parse `Last Updated` as a datetime:** Currently stored as a raw string. Converting it to `datetime` enables recency analysis (e.g. are recently updated apps rated higher?) and makes the column usable in time-series or filtering operations without extra work for downstream users.
- **Cap or flag outlier ratings:** The Play Store dataset is known to contain ratings above 5.0 due to data entry errors. Add a validation step that flags or drops any `Rating` value outside the `[1.0, 5.0]` range before computing means or distributions.
- **Deduplicate app records:** The dataset contains duplicate `App` entries (same app name, different records). Decide on a deduplication strategy (e.g. keep the most-installed record, or keep all) and document it clearly, as duplicates can skew category-level averages.

### 2. Repository Structure

- **Do not commit `googleplaystore.csv` directly to the repo** if it is large (it is ~6 MB). Instead, add a download instruction pointing to the original Kaggle source, or use a `data/` folder with a `README.md` explaining where to obtain it:

  ```
  data/
  └── README.md   # Instructions: download from https://www.kaggle.com/datasets/lava18/google-play-store-apps
  ```

- **Adopt a standard project layout:**

  ```
  ├── data/
  │   ├── raw/                  # Original googleplaystore.csv (or download instructions)
  │   └── processed/            # Cleaned dataset after pipeline runs
  ├── notebooks/
  │   └── googleplaystoredaTA.ipynb
  ├── src/                      # Reusable helper functions (clean_size, clean_installs, clean_reviews)
  │   └── cleaning.py
  ├── outputs/
  │   └── size_distribution.png # Saved matplotlib charts
  └── README.md
  ```

- **Fix the notebook filename casing:** `googleplaystoredaTA.ipynb` has inconsistent capitalisation. Rename it to `google_playstore_eda.ipynb` or similar for professionalism and cross-platform compatibility (Linux filesystems are case-sensitive).
- **Add a `.gitignore`:** Exclude `__pycache__/`, `.ipynb_checkpoints/`, `*.pyc`, and any local virtual environment folders.

### 3. Documentation

- **Add a `requirements.txt`:** Pin the exact versions used so the notebook is reproducible across machines:

  ```
  pandas==2.x.x
  numpy==1.x.x
  matplotlib==3.x.x
  ```

- **Document all cleaning functions inline:** `clean_size()`, `clean_installs()`, and `clean_reviews()` are core to this project. Add docstrings explaining inputs, outputs, edge cases handled, and any values mapped to `NaN`.
- **Add a cleaned dataset export step:** At the end of the cleaning pipeline, save the processed DataFrame to `data/processed/googleplaystore_clean.csv` so users who only want the clean data do not need to re-run the full notebook.
- **Save visualisations as image files:** The current histogram is rendered inline. Add `plt.savefig('outputs/size_distribution.png', dpi=150, bbox_inches='tight')` before `plt.show()` so charts are available in the repo for README previews and reports.
- **Embed a chart preview in the README:** Reference the saved histogram image directly in the README with `![App Size Distribution](outputs/size_distribution.png)` to make the project visually engaging on GitHub.

### 4. Ethics, Privacy & Attribution

- **Cite the original dataset source:** The dataset is publicly available on Kaggle. Add the full attribution:
  > Lavanya M. (2019). *Google Play Store Apps.* Kaggle. Available at: https://www.kaggle.com/datasets/lava18/google-play-store-apps
- **Note the dataset's age:** The Kaggle dataset was scraped in 2018–2019. App market conditions have changed significantly since then — add a visible warning in the README and at the top of the notebook that findings reflect a historical snapshot and should not be used for current market strategy without refreshed data.
- **Add a `LICENSE` file:** For an analytical/educational project, an **MIT License** for the code and notebooks is standard. Since the underlying dataset is third-party, note clearly that the license covers only your analysis code, not the raw data itself.

### 5. Analysis Quality Improvements

- **Report the mean rating with context:** The mean Play Store rating is well-known to be inflated (~4.17) due to survivorship bias (low-rated apps get delisted). Add a note on this limitation alongside the mean value.
- **Extend the top-apps analysis beyond top 5:** The top 5 most-installed apps are dominated by Google's own pre-installed applications. Consider filtering out system/pre-installed apps (identifiable by developer name or `Category == 'COMMUNICATION'` + very high installs) to surface the most-installed third-party apps — a more useful competitive benchmark.
- **Add a category-level summary table:** A grouped DataFrame showing, per category: app count, mean rating, median installs, and Free/Paid split would be a high-value addition that many GitHub users look for in Play Store EDA projects.
- **Quantify the data quality issues:** Rather than describing anomalies in prose, add a dedicated "Data Quality Report" cell in the notebook that prints: total rows, rows dropped per cleaning step, columns with null percentages, and any values coerced. This builds credibility and transparency.
- **Consider adding a correlation analysis:** Explore whether `Size`, `Reviews`, `Installs`, or `Last Updated` recency correlate with `Rating`. Even a simple correlation matrix would add analytical depth and is straightforward to implement with `df.corr()`.


## Author

**[Mohd Faiz]**

- **Role:** Business and Data Analyst
- **GitHub:** [https://github.com/faizikbal01-lab](https://github.com/your-github-handle)

---

*Disclaimer: This analysis is based on a publicly available Google Play Store dataset and is intended for educational and research purposes only. App market conditions and store listings change frequently; findings should not be used as the sole basis for product or investment decisions.*

