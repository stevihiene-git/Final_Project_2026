# A Stacked Ensemble Approach for Detecting Suspicious Uniform Resource Locators (URLs) on the Reddit Social Network

**Author:** Oduh, Ihiene Stephen  
**Matriculation Number:** 249074080  
**Supervisor:** Dr. N. A. Azeez  
**Head of Department:** Prof. C. O. Yinka-Banjo  
**Institution:** Department of Computer Sciences, University of Lagos, Akoka, Yaba, Lagos, Nigeria  
**Degree:** Master of Information Technology (MIT)  
**Date:** September 2026  

---

## 📌 Abstract Overview

The rapid expansion of social media has heightened the spread of deceptive and malicious links. Detecting suspicious URLs on platforms like Reddit presents unique challenges due to high volumes of user-generated content and platform-specific dynamics. Standard detection approaches relying purely on URL-lexical features often miss critical social context.

This research introduces a novel **Stacked Ensemble** architecture that combines URL-lexical properties with Reddit-specific contextual signals (account metrics, post interaction signals, and community phishing rates). Utilizing a dataset of **19,870 enriched observations**, six diverse base machine learning models were evaluated alongside four combination meta-learning strategies.

The **Logistic Regression stacked ensemble** demonstrated superior discrimination performance (87.30% accuracy, 79.68% precision, 89.25% AUC, and 0.559 MCC) while significantly minimizing false positive alerts (3.13% FPR) compared to individual classifiers.

---

## 📊 Dataset Structure

The project uses an enriched dataset comprising **19,870 instances** across **15 variables** (1 Post ID identifier, 13 predictor features, and 1 binary target label).

* **Identifier:** `PostID` (record identifier, excluded from model training)
* **Target Label:** `label` (Binary: `0` = Legitimate, `1` = Suspicious / Phishing)

### Feature Breakdown (13 Predictors)
1. **URL-Level Features (5):** `link_length`, `has_https`, `num_dots`, `num_digits`, `num_special_chars`, `domain_length`
2. **Account-Level Features (3):** `username_length`, `username_num_digits`, `account_age`
3. **Post-Level Features (3):** `title_length`, `post_score`, `comment_count`
4. **Community-Level Feature (1):** `subreddit_phish_rate` (fold-aware historical community risk score)

---

## 🤖 Model Architecture

### First-Level (Base) Classifiers
1. **AdaBoost** (Decision stump base estimators)
2. **Gradient Boosting** (Stage-wise additive decision trees)
3. **Random Forest** (Bootstrap aggregation of decision trees)
4. **Linear Support Vector Machine (SVM)** (Calibrated via Platt scaling for probability outputs)
5. **Decision Tree** (Entropy / Information Gain splitting)
6. **Gaussian Naïve Bayes** (Probabilistic classifier handling continuous features)

### Meta-Learner (Level-2)
* **Logistic Regression Meta-Learner:** Trained on out-of-fold (OOF) probability predictions generated during 5-fold cross-validation to prevent data leakage.
* **Baseline Voting Combinations (for comparison):** Uniform Majority Voting, Accuracy-Weighted Voting, and Exponential Accuracy-Weighted Voting.

---
🚀 Reproducibility: Setup, Installation & Execution

Follow these steps to reproduce the experiments and results presented in Chapter 4.

1. Prerequisites
2. 
Python 3.9–3.12

Git and pip


Required raw datasets: new_all_posts.csv and reddit_post_features.csv

3. Clone the Repository
   
git clone https://github.com/stevihiene-git/Final_Project_2026.git

cd Final_Project_2026

Place the two required CSV files inside the uploads/ directory.

5. Set Up the Environment
Windows (PowerShell):

python -m venv venv

venv\Scripts\Activate.ps1

Linux/macOS:

python3 -m venv venv

source venv/bin/activate

Install dependencies:

pip install -r requirements.txt

4. Build the Corrected Dataset
   
python build_dataset.py --uploads_dir uploads --out enriched_dataset_final.csv

Expected output: 19,870 observations, comprising 17,831 legitimate and 2,039 suspicious posts.

The script corrects URL feature extraction and CSV data-quality issues before generating the enriched dataset.

6. Run the Machine Learning Pipeline
   
python reddit_phishing_pipeline.py --data enriched_dataset_final.csv --out results

The pipeline balances classes, trains and evaluates six baseline classifiers, implements four stacking ensemble strategies, and generates performance comparisons.

The balanced modelling dataset contains 10,195 observations (8,156 legitimate and 2,039 suspicious posts).

7. Generated Results

