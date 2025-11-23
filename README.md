# BT4012 Fraud Analytics, AY2025/2026 – Group 16  

Fake Job Posting Detection and Analysis

We use the **Employment Scam Aegean Dataset (EMSCAD)**, available on Kaggle:

https://www.kaggle.com/datasets/shivamb/real-or-fake-fake-jobposting-prediction/data

This repository contains the codes for our project on **automatic detection and analysis of fake online job postings**. We combine:

- **Classical machine learning models** trained on rich engineered features and text embeddings (with pre-trained BERT)
- **Transformer-based models** (BERT, RoBERTa, DistilBERT) fine-tuned end-to-end on raw text  
- **Unsupervised clustering** of fraudulent postings to uncover fraud subtypes and behavioural patterns

Our primary goal is to **protect job seekers** by developing high-recall fraud detectors and providing interpretable insights into common scam patterns.

---

## 1. Project Overview

- **Problem.** Online job scams mimic legitimate postings but are designed to steal data, extort money, or coerce victims, leading to significant financial and identity harm.
- **Dataset.** EMSCAD contains **17,880 job postings** (17,014 legitimate, 866 fraudulent; ~4.8% fraud rate) with 18 attributes spanning long text fields and structured metadata. 
- **Approach.**
  1. Build binary classifiers to detect fake postings
  2. Perform clustering on fraudulent postings to derive **fraud subtypes** and red-flag patterns

---

## 2. High-Level Findings

### **Model Performance**
- **BERT-base** achieved the best overall balance of **PR-AUC, F1-score, and recall**, making it the strongest standalone detector.
- **DistilBERT** delivered competitive performance with roughly half of BERT’s computational cost.
- **RoBERTa-base** performed well but slightly below BERT in PR-AUC and recall.
- Among the baseline classical models, **LightGBM** performed strongly and when trained on engineered features and pre-trained BERT text embeddings.
- A **stacked ensemble** of LightGBM + Random Forest + MLP with Logistic Regression as the meta-classifier achieved the **highest recall** across all classical models, though at the cost of lower precision.

### **Fraud-Related Patterns**
Across EDA, engineered features, and transformer embeddings, fraudulent postings consistently showed:
- **Short, low-effort company profiles** with minimal text  
- Over-use of **remote work**, **flexible timing**, and **generic role descriptions**  
- Suspicious linguistic cues such as excessive action verbs, digit-heavy titles, or vague responsibilities  
- **Missing company metadata** (logo, profile, headquarters) strongly correlated with fraud  
- Clustering revealed common scam themes, including:
  - “Work-from-home / flexible hours” scams  
  - “Quick cash / no experience needed” postings  
  - Impersonation of reputable industries (engineering, cruise, finance)  

These insights help interpret model predictions and support real-world moderation workflows.

---

## 3. Repository Structure

```text
.
├─ 01_eda_and_feature_engineering.ipynb
├─ 02_feature_selection.ipynb
├─ classical/
│  └─ classical_machine_learning_models.ipynb
├─ transformers/
│  ├─ basebert_codes.ipynb
│  ├─ roberta_codes.ipynb
│  ├─ distilbert_codes.ipynb
│  └─ berts_comparison.ipynb
├─ clustering/
│  └─ clustering_analysis_of_fraudulent_listings.ipynb
│
└─ README.md

