# Double Machine Learning (DML) – Causal Inference Project

This project implements *Double Machine Learning (DML)* to estimate the *Average Treatment Effect (ATE)* and analyze *Heterogeneous Treatment Effects (CATE)* using a synthetic dataset.

---

## 📘 Contents
- dml_causal_inference.ipynb — Main notebook with data generation, DML estimation, CATE analysis, sensitivity checks, and plots.
- requirements.txt — Python dependencies.
- report/ — Final project report (optional).
- figures/ — Saved plots (optional).

---

## 🧠 Methods Used
- Synthetic dataset with 3000 samples & 50 confounders  
- Random Forest models for:
  - Outcome prediction \(E[Y|X]\)
  - Treatment prediction \(E[T|X]\)
- 5-fold cross-fitting  
- Residual-on-residual regression (DML ATE)  
- T-Learner for CATE estimation  
- OLS comparison + sensitivity analysis  

---

## ▶️ Run Instructions
Install dependencies:

```bash
pip install -r requirements.txt
