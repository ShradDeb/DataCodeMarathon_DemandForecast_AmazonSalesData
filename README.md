# Amazon Product Demand Forecasting (Cross-Sectional)

This project predicts **product demand** (using `rating_count` as a demand proxy) based on product attributes, prices, discounts, ratings, categories, and review text features from an Amazon dataset.

---

## 🚀 Project Overview
Typical retail demand forecasting uses time series of daily/weekly sales.  
Here we predict *relative demand across products* instead:
- **Target**: `rating_count` (number of reviews, a strong proxy for total sales)
- **Goal**: Estimate how pricing, discounts, ratings and review sentiment influence demand and perform "what-if" scenarios like a 10% price cut.

---

## 📂 Dataset
- **Source**: Cleaned Amazon dataset (1465 rows)
- **Columns include**:
  - Product attributes: `product_name`, `category`
  - Pricing: `discounted_price`, `actual_price`, `discount_percentage`
  - Reviews: `rating`, `rating_count`, `review_title`, `review_content`
  - Text: `about_product`

---

## 🧹 Data Cleaning & Preprocessing
1. Converted prices and discounts from strings with currency symbols into numeric values.
2. Converted ratings and rating counts to numeric (filling missing values appropriately).
3. Aggregated multiple rows per product into one product-level row.
4. Created `full_review` by combining review title and content.
5. Engineered text-based features:
   - Cleaned text (lowercase, removed punctuation)
   - Word counts: `about_len`, `review_len`
   - Sentiment features: positive/negative word counts and `sentiment_delta`.

---

## 🔍 Exploratory Data Analysis (EDA)
- Histograms of product demand (`rating_count`) and its log transform to reduce skew.
- Scatter plots of:
  - Discounted price vs demand
  - Discount percentage vs demand
  - Rating vs demand
- Category-level analysis of average demand.
- Correlation heatmaps to find key drivers.
- Outlier and Pareto analysis to show how a few products drive most demand.

---

## 🤖 Machine Learning Model
- **Algorithm**: Gradient Boosting Regressor
- **Input Features**:
  - Numeric: price, discount, rating, word counts, sentiment metrics
  - Categorical: top 20 categories (others grouped as "Other")
- **Target**: log1p(rating_count)
- **Pipeline**: Preprocessing (imputation + one-hot encoding) → Gradient Boosting
- **Performance**:
  - R² (log scale): ~0.31
  - RMSE: ~28k reviews
  - MAE: ~11k reviews

---

## 💡 What-If Price Simulation
Simulates a 10% price cut for top-demand products and estimates new demand.  
Reveals price elasticity (e.g., some products show ~28% predicted increase in demand).

---

## 🗂️ Repository Structure
```
.
├── amazon.csv                         # Original dataset
├── amazon_product_level.csv            # Cleaned & aggregated dataset
├── feature_importances.csv             # Model's feature importance
├── price_cut_scenario_top5.csv         # Price-cut scenario analysis
├── demand_model_pipeline.pkl           # Saved trained model
├── notebooks/
│   └── amazon_demand_forecast.ipynb    # End-to-end notebook
└── README.md                           # Project documentation (this file)
```

---

## ⚙️ How to Run
1. Clone the repo:
   ```bash
   git clone https://github.com/<your-username>/amazon-demand-forecast.git
   cd amazon-demand-forecast
   ```
2. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```
3. Open the notebook:
   ```bash
   jupyter notebook notebooks/amazon_demand_forecast.ipynb
   ```
4. Run all cells to reproduce cleaning, EDA, modelling and scenario analysis.

---

## 🏆 Key Learnings
- Price, discount and rating strongly influence review counts.
- Text sentiment and description length add meaningful predictive power.
- Scenario planning shows which products respond best to pricing changes.

---

## 📌 Next Steps
To build a true time-series demand forecast, add:
- Date-wise sales quantities
- Promotion and marketing spend
- Stock levels and seasonality features

Then use ARIMA, Prophet, or advanced ML (XGBoost, LSTM) to forecast future daily/weekly demand.

---

## 🙋‍♀️ Author
**Shraddha Debata**  
Data Analyst | Data Scientist  
Passionate about data-driven decision making and business analytics.

