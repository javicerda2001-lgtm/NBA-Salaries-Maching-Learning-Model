# Decoding Value in the NBA: A Machine Learning Financial Appraisal Engine

This repository contains the source code and academic framework for the Master's Thesis  presented for the Master in Business Analytics at UNIE Universidad. 

**Thesis Title:** *Optimization of Financial Appraisal Models in the NBA through PCA and Clustering: Decoding Performance Value in the Positionless Basketball Era.*  
**Author:** Javier Cerdà Llopis  

---

## 📌 Executive Summary
The modern NBA operates as a highly complex financial ecosystem governed by a soft Salary Cap. However, the labor market exhibits critical inefficiencies due to contracts signed based on subjective perceptions or obsolete positional labels (PG, SG, SF, PF, C).

<img width="567" height="270" alt="Captura de pantalla 2026-06-30 a las 11 20 03" src="https://github.com/user-attachments/assets/ac45c0d6-6322-41ad-9855-7158b0c4812f" />


This project delivers a **Minimum Viable Product (MVP)** consisting of an advanced financial appraisal engine designed to audit and predict the true market value of players. By shifting from nominal dollar salaries to a deflation technique based on **Percentage of the Salary Cap (% Cap)**, the model normalizes 25 years of historical data (2000–2025). Utilizing **Principal Component Analysis (PCA)** and **Unsupervised K-Means Clustering**, the engine segments the league into 4 latent functional roles suited for the *Positionless Basketball* era, removing administrative biases. Finally, a **Random Forest Regressor** achieves a robust **$R^2$ score of 0.73** on temporal validation, identifying deep structural market inefficiencies.

---

## 🛠️ Technical Architecture & Methodology

The project's pipeline is divided into four main modular phases:

1. **Data Engineering & Deflation:** 
   * Merging 25 years of box score statistics (Kaggle/GitHub) with financial metrics (HoopsHype).
   * Filtering statistical noise by establishing a strict playtime threshold ($MP \ge 10$).
   * Implementing feature engineering to combat salary cap inflation via the relative budgetary impact formula:
     Impacto presupuestario % Cap = Salario Jugador / Salary cap temporada 

2. **Dimensionality Reduction (PCA):** 
   * Addressing severe multicollinearity (e.g., strong correlations between Minutes Played, Usage Rate, and Points).
   * Projecting 20 standard and advanced box-score variables into **6 orthogonal Principal Components**, retaining over **80% of the cumulative variance** while purifying the statistical signal.

3. **Unsupervised Functional Clustering:**
   * Determining the hyperparameter $k=4$ through the **Elbow Method** and **Silhouette Score optimization** (improving from 0.170 to 0.223 post-PCA).
   * Defining 4 distinct macro-roles: 
     * *Cluster 3: Offensive Superstars / Playmakers* (Elite metrics, highest cap hit).
     * *Cluster 2: Versatile Role Players* (Consistent, complete, and mathematically the most undervalued asset class).
     * *Cluster 0: Defensive Anchors / Rim Protectors* (High efficiency near the basket, high rebounding/blocking).
     * *Cluster 1: Depth Rotations / Bench Support* (Low volume but efficient per-minute output).

4. **Supervised Regressive Ensemble:**
   * Training a **Global Random Forest Regressor** incorporating the engineered `Cluster_PCA` label as an interactive predictor variable.
   * Applying **Temporal Out-of-Sample Validation** (training on 2000–2024, testing blindly on the 2025 season) to emulate real-world Front Office operations and eliminate data leakage.

---

## 📈 Key Findings & Market Auditing

* **Predictive Precision:** The final ensemble model yields a Median Absolute Error (**MedAE**) of **$3.30M**, translating to a minute 2.3% margin of error relative to a standard $140M franchise budget.
* **The "Cluster 2" Value Asymmetry:** While the market for superstars (Cluster 3) is highly efficient (3.17% variance), **Cluster 2 (Versatile Role Players) exhibits a massive structural undervaluation of -30.03%**. The model isolates elite perimeter spacing (3P%) and quiet defensive contributions (STL/BLK) as highly mispriced traits in Free Agency, providing a pure financial arbitrage opportunity for General Managers.

---

## 📂 Repository Structure

```text
├── data/
│   ├── raw/            # Verbatim: "NBA Player Stats and Salaries_2000-2025.csv" & "NBA SALARY CAP TFM.csv"
│   └── processed/      # Scaled features and target % Cap transformations
├── notebooks/          # Step-by-step Jupyter Notebooks (EDA, PCA, K-Means, Random Forest)
├── src/                # Modular Python scripts for pipeline execution
├── documents/          # Verbatim: "TFM_Javier_Cerdà.pdf" & "Modelo-de-Tasacion-Financiera-en-la-NBA-con-Clustering.pdf"
├── requirements.txt    # Production environment dependencies (scikit-learn, pandas, etc.)
└── README.md           # Project presentation


