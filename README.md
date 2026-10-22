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

## 🚀 Setup & Installation

### Prerequisites
* **Python:** Version 3.9 or higher
* **Git**

### 1. Clone the Repository
```bash
git clone [https://github.com/stevihiene-git/final-project-2026.git](https://github.com/stevihiene-git/final-project-2026.git)
cd final-project-2026




