# CSDA Coursework – Statistical Modelling & Machine Learning (R)

This repository contains the full coursework completed for the **Computational Statistics & Data Analysis (CSDA)** module at Nottingham Trent University.  
It includes **three major statistical modelling tasks** implemented entirely in **R**, covering:

1. Hidden Markov Models (HMM) for gene prediction  
2. Expectation–Maximization (EM) for latent variable estimation  
3. Missing data imputation + K-means clustering for diabetes risk analysis  

> 📄 Full coursework documentation: `docs/CSDA_Coursework_Report.pdf`

---

# 📘 Overview of Tasks

## ✅ **Task 1 — Predicting Coding vs. Non-Coding Regions (HMM)**

### **Goal**
Use a **two-state Hidden Markov Model** to classify each nucleotide in the *Pectobacterium phage KU574722.1* genome as:

- **Coding**
- **Non-coding**

### **Methods**
- Extracted CDS regions from GenBank  
- Calculated emission probabilities for A/C/G/T in each state  
- Constructed 2×2 transition matrix (best switch probability **p = 0.033**)  
- Applied **Viterbi algorithm** for decoding  
- Performed sliding-window **triplet entropy analysis**  

### **Results**
- **Accuracy: 71.52%**  
- Confusion matrix shows bias towards predicting coding regions  
- Accuracy decreased as p increased (Figure 2)  
- Triplet entropy difference between coding & non-coding: **0.1%**  
- t-test: **p = 0.479** → not significant  
- Entropy correlation with coding status: **0.014**

### **Conclusion**
A simple HMM can moderately identify gene regions, but lacks codon-level modelling and misses many coding bases.  
Entropy alone is **not** a reliable predictor for this genome.

---

## ✅ **Task 2 — Estimating Vaccine Effectiveness (EM Algorithm)**

### **Goal**
Estimate the effectiveness of two vaccines (A & B) given:

- 5 sites  
- Known outcomes (flu/no flu)  
- Unknown vaccine type at sites 2–5  
- Only site 1 is labeled as using vaccine A  

### **Methods**
- Defined latent variable **Zᵢ ∈ {A, B}** for each site  
- E-step: computed posterior probability **wᵢ = P(Zᵢ = A | data)**  
- M-step: updated parameters  
  - Vaccine A effectiveness (**pA ≈ 0.82**)  
  - Vaccine B effectiveness (**pB ≈ 0.36**)  
  - Prior **π**  
- Iterated until convergence

### **Results**
- Sites **1, 2, 4**: almost certainly vaccine A  
- Sites **3, 5**: almost certainly vaccine B  
- Vaccine A far superior (~82% protection)  
- Vaccine B significantly weaker (~36% protection)  

### **Conclusion**
EM successfully recovers latent vaccine types and their effectiveness.  
Useful for modelling hidden groupings in small datasets.

---

## ✅ **Task 3 — PMM Imputation + Diabetes Clustering**

### **Goal**
Explore diabetes risk factors using:

1. **Predictive Mean Matching (PMM)** imputation  
2. **K-means clustering (k=2)**  
3. Evaluation via internal & external metrics  

### **Methods**

#### **Missing Data Imputation**
- Used **mice** package  
- Replaced insulin=0 with PMM-predicted values  
- All 6 missing insulin values successfully imputed

#### **Clustering**
- K-means (k=2) chosen using:
  - Elbow method (clear bend at k=2)
  - Silhouette analysis (highest at k=2)
- Evaluated using:
  - **F-measure = 0.8205**  
  - **Accuracy = 76.67%**  
  - **Silhouette = 0.2418**  
  - **Dunn Index = 0.0855**  

### **Results & Visual Insights**
- PCA scatterplot shows clear separation between clusters (Figure 10)  
- Patients with higher glucose levels cluster strongly with diabetes-positive cases  
- High clinical relevance: clustering algorithm effectively groups high-risk patients  

### **Conclusion**
PMM preserves statistical distribution and relationships in data.  
K-means clustering provides meaningful insight into diabetes risk indicators.
