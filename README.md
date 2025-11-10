
---

## 💹 2️⃣ **Optiver – Trading at the Close introduction data**
**Repository name suggestion:** `optiver-trading-analysis`

```markdown
# 💹 Optiver - Trading at the Close (Financial Data Analysis)

This project analyzes stock market data from **Optiver’s Trading at the Close dataset** to understand and model trading patterns during market closing times.

---

## 🎯 Objective
The goal is to explore relationships between price, volume, and volatility in the last minutes of trading, and develop insights or predictive signals.

---

## 📂 Dataset
- **Source:** Financial data sample (Optiver / Kaggle)  
- **Features:** `bid_price`, `ask_price`, `volume`, `seconds_in_bucket`, `target`  
- **Size:** ~40,000 records  

---

## ⚙️ Tools & Libraries
- Python 3  
- Pandas, NumPy  
- Matplotlib, Seaborn  
- Scikit-learn  

---

## 🧩 Workflow
1. **Data Cleaning**
   - Handled missing values and duplicate rows  
   - Converted timestamps to datetime objects  

2. **Exploratory Data Analysis**
   - Price movement visualization  
   - Volume spikes near market close  

3. **Feature Engineering**
   - Lag features, moving averages, volatility measures  

4. **Modeling**
   - Regression models (Linear Regression, Random Forest)  
   - Cross-validation for performance estimation  

5. **Evaluation**
   - RMSE, R² score, residual analysis  

---

## 📈 Key Insights
- Significant trading volume surge during final 10 minutes  
- Spread between bid and ask prices narrows near market close  
- Volatility predicts end-of-day price adjustments  

---

## 🧠 Results
- **Best Model:** Random Forest Regressor  
- **R² Score:** 0.78  

---

## 🚀 How to Run
```bash
pip install pandas numpy scikit-learn matplotlib seaborn
jupyter notebook Optiver_Trading_Analysis.ipynb
