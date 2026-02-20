
# Customer Churn Prediction

Predicting telecom customer churn with **90% recall** using XGBoost and cost-optimized threshold tuning.

## 🎯 Results

| Model | Accuracy | Precision | Recall | F1 | ROC-AUC |
|-------|----------|-----------|--------|-----|---------|
| Baseline | 73% | 0% | 0% | 0% | 0.50 |
| **XGBoost (threshold=0.5)** | 75% | 52% | 78% | 62% | **0.84** |
| **XGBoost (threshold=0.3)** | 68% | 45% | **90%** | 60% | **0.84** |

**At optimal threshold (0.3):**
- Catches **90% of churners** (335 out of 374)
- Only misses 39 customers ($46,800 in lost value)
- Creates 411 false alarms ($20,550 in wasted offers)
- **Total cost: $67,350** vs $113,000 at default threshold
- **Saves $45,650** through threshold optimization

---

## 🔍 Key Insights

### Top Churn Predictors
1. **Contract type** (combined importance: 0.53)
   - Month-to-month: 43% churn
   - Two-year: 3% churn
2. **Fiber optic internet** (importance: 0.27)
   - 42% churn rate (vs 19% for DSL)
3. **Low tenure** (importance: 0.01)
   - 68% of churners leave in first 12 months

### Business Impact
- **Target:** 400 high-risk customers/month
- **Investment:** $20,000/month in retention offers
- **Return:** $108,000/month in prevented churn
- **ROI:** 5.4x
- **Annual savings:** ~$547,000

---

##  Dataset

- **Source:** IBM Telco Customer Churn
- **Size:** 7,043 customers
- **Features:** 20 (demographics, services, account info)
- **Target:** Churn (Yes/No)
- **Class distribution:** 73% stayed, 27% churned

---

##  Tech Stack

- **Python 3.x**, Pandas, NumPy
- **Scikit-learn** - preprocessing, metrics, train/test split
- **XGBoost** - gradient boosted trees with scale_pos_weight
- **Matplotlib, Seaborn** - visualization

---

##  Project Structure
```
├── churn_analysis.ipynb    # Main analysis notebook
├── README.md               # This file
├── requirements.txt        # Dependencies
└── .gitignore
```

---

##  Usage
```bash
# Clone repository
git clone https://github.com/Dereger325/churn-data-prediction.git
cd churn-data-prediction

# Install dependencies
pip install -r requirements.txt

# Download dataset from Kaggle
# https://www.kaggle.com/datasets/blastchar/telco-customer-churn

# Run notebook
jupyter notebook churn_analysis.ipynb
```

---

## Model Performance Details

### Confusion Matrix (Threshold = 0.3)
```
                Predicted
              No      Yes
Actual No   [624]   [411]   ← 411 false alarms
Actual Yes  [39]    [335]   ← Caught 335/374 churners (90%)
```

### Why Threshold 0.3?
- Each missed churner costs $1,200 (lifetime value)
- Each false alarm costs $50 (retention offer)
- **Cost ratio:** 24:1 → optimize for recall, accept lower precision
- Threshold 0.3 minimizes total business cost

---

##  Key Learnings

1. **Accuracy is misleading** for imbalanced data (73% baseline just predicts majority class)
2. **Business context drives threshold** - default 0.5 rarely optimal
3. **Feature engineering matters** - PricePerService captured value perception
4. **scale_pos_weight critical** for handling 73/27 class imbalance in XGBoost
5. **Contract type dominates** - single most important business lever

---

##  Week 1 of Month 2 - ML Learning Journey

**Days 1-7 breakdown:**
- Day 1: Data loading and exploration
- Day 2: Visualization and pattern analysis  
- Day 3: Data cleaning, encoding, feature engineering
- Day 4: Baseline model and train/test split
- Day 5: Confusion matrix and threshold tuning
- Day 6: Feature importance and ROC curve
- Day 7: Business recommendations and deployment strategy

**Time invested:** 30-45 min/day × 7 days = 3.5-5 hours  
**Outcome:** Production-ready churn prediction model with actionable business insights

---

##  Next Steps

- [ ] Deploy model predictions to CRM
- [ ] A/B test retention offers
- [ ] Monthly model retraining pipeline
- [ ] Investigate fiber optic churn drivers
- [ ] Launch contract conversion campaign

---

**Author:** [Dereger]   
**GitHub:** [github.com/Dereger325](https://github.com/Dereger325)

---

*Built with focus on business impact, not just model accuracy.*