# Spotify/Sparkify Customer Churn Prediction

## Project Overview

This project aims to predict customer churn for a music streaming service (Sparkify, similar to Spotify). By analyzing user interactions, subscription information, and listening habits, we identify users at risk of canceling their subscription.

The dataset is fictional and generated for the Udacity Data Science Nanodegree program. It includes JSON logs of user sessions, capturing song plays, account actions, and user demographics.

---

## Dataset

* **Source:** Udacity Nanodegree – Sparkify Mini Dataset
* **Format:** JSON file (`mini_sparkify_event_data.json`)
* **Records:** ~286,500 user events
* **Columns include:**

  * `userId`, `sessionId`, `page`, `auth`, `level` (free/paid), `location`, `userAgent`
  * `artist`, `song`, `length`
  * `ts` (timestamp), `registration`, `gender`, `churn` (derived)

### Key Insights

* Tracks user behavior, session activity, and song plays.
* Can analyze artist popularity, device/browser usage, subscription behavior, and geographical trends.

---

## Project Workflow

### 1. Data Loading

* Loaded JSON dataset using pandas.
* Initial exploration included checking data types, missing values, and duplicates.

### 2. Data Cleaning and Preprocessing

* Dropped rows with missing `userId` (~2.9% of data).
* Converted timestamps to datetime objects.
* Filled missing values for demographic and song-related data.
* Converted `userId` to numeric type for aggregation.

### 3. Outlier Analysis

* Numeric columns analyzed using IQR, Z-score, and modified Z-score methods.
* Visualized distributions with box plots, violin plots, and histograms.
* Outliers were capped to reduce skew.

### 4. Exploratory Data Analysis (EDA)

* Defined churn as users who had a `Cancellation Confirmation` event.
* Churn rate: ~23%.
* Visualized page events, subscription levels, daily active users, and user engagement metrics.
* Correlation analysis identified features most associated with churn.

### 5. Feature Engineering

* Created user-level aggregations: `total_sessions`, `engagement_days`, `total_events`, `total_songs_played`, `unique_artists`, `unique_songs`.
* Derived additional features:

  * `song_play_ratio` (songs/events)
  * `artist_diversity` (unique_artists/songs)
  * `engagement_intensity` (events per day)
  * `thumbs_up_ratio`
  * `error_rate`

### 6. Model Development

* Models evaluated:

  * Logistic Regression
  * Random Forest Classifier
  * Gradient Boosting Classifier
  * XGBoost Classifier
* Used train-test split and cross-validation for evaluation.
* Metrics considered: Accuracy, Precision, Recall, F1-score, ROC-AUC.
* Feature importance analyzed using SHAP.

### 7. Results

* Models successfully identified users likely to churn.
* Important predictive features: engagement intensity, session activity, playlist actions, thumbs-up/down behavior.
* Insights can help Sparkify design retention strategies.

---

## How to Run

1. Clone the repository.
2. Place the `mini_sparkify_event_data.json` file in the working directory.
3. Run the Jupyter Notebook (`Churn_Prediction_Sparkify.ipynb`) step by step.
4. Ensure all required libraries are installed (pandas, numpy, matplotlib, seaborn, scikit-learn, xgboost, shap, etc.).

---

## Dependencies

* Python 3.8+
* pandas
* numpy
* matplotlib
* seaborn
* scikit-learn
* xgboost
* shap (optional for feature importance visualization)

---

## Future Work

* Incorporate more advanced feature engineering such as session time patterns or network graph of friends.
* Test additional models like LightGBM or CatBoost.
* Deploy a real-time churn prediction system for dynamic retention campaigns.
