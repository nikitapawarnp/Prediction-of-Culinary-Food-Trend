# Predicting Emerging Food Trends

> Forecasting dish & cuisine momentum from Yelp reviews using NLP, networks, clustering, and deep learning.

---

## 📌 Project Overview

This repository analyzes Yelp restaurant reviews to **discover and forecast emerging food trends**. We combine classic NLP (keyword/NER/topic models), **co-occurrence networks**, **K-Means clustering**, and **time-series forecasting (LSTM/Prophet)** to turn unstructured text into **actionable insights** for restaurants, suppliers, and investors. Philadelphia is used as a pilot market due to its diverse food scene and rich review density.&#x20;

---

## 🎯 Research Questions

1. **What cuisines and dishes are trending** and how do they evolve over time?
2. **Which items co-occur** (are ordered/mentioned together) and how can that inform **menu combos**?
3. Can we **segment restaurants** (value vs premium vs niche) from review/metadata patterns?
4. How well can we **forecast demand** for dishes using review-time signals?
5. How do topic proportions and named entities **validate trend shifts**?&#x20;

---

## 💡 Why It Matters

* **Restaurants & food brands:** plan menus, pricing, promos, and new launches with data.
* **Suppliers:** translate trend signals into **ingredient demand** and inventory plans.
* **Investors & operators:** identify **growth categories** and neighborhood opportunity zones.
* **Platforms:** improve **search, recommendations, and merchandising**.&#x20;

---

## 🧱 Data & Preprocessing (Philadelphia pilot)

* **Source:** Yelp business + review data (restaurants only), filtered to **open businesses**, **useful>0**, **stars > 3**, **2013–2016**, monthly rollups.
* **Final working table:** **117,869 rows × 8 columns** after merges/filters and CSV extraction for faster iteration.
* Rationale: positive experiences are more likely to seed sustained trends; 2013–2016 chosen to avoid major exogenous shocks.&#x20;

---

## 🛠️ Methodology

1. **Keyword Frequency Analysis**
   Monthly token pipelines to track **dish/cuisine mentions** and seasonality.&#x20;
2. **Named Entity Recognition (NER)**
   Extract dish/cuisine entities (e.g., *pizza, ramen, tacos, sushi; American, Japanese, Italian, Mexican*).&#x20;
3. **Topic Modeling (LDA)**
   12-topic model; absolute & relative topic-share shifts (2013→2015) to quantify momentum.&#x20;
4. **Dish Co-occurrence Network**
   Graph of dishes mentioned together → **combo design** and **cross-sell** candidates (e.g., *dumplings–ramen–hotpot*, *BBQ–fried chicken*).&#x20;
5. **K-Means Clustering (K=4)**
   Segments: budget, mid-range, premium, specialty/niche (chosen via SSE elbow).&#x20;
6. **Time-Series Forecasting**

   * **LSTM** on monthly dish series (2013–2016).
   * **Prophet** for multi-dish baselines and seasonality diagnostics.
   * Report **MAE** by item; beverages (e.g., *smoothies, latte, espresso, matcha*) forecast best.&#x20;
7. **External Cross-Validation**
   **Google Trends** and **brand comps (e.g., Chipotle)** to verify directionality (e.g., **tacos up** vs **sushi slower**).&#x20;

---

## 🔑 Key Results (Highlights)

* **Risers & Newcomers:** **tacos, dumplings, burgers, cocktails** show strong upward momentum; **salads/coffee/steak** remain very popular.&#x20;
* **Stable Core:** **pizza, pasta, waffles** show steady baseline demand.&#x20;
* **Seasonality:** **desserts & pasta** peak in winter; **ramen & seafood** display distinct seasonal curves.&#x20;
* **Co-ordering:** tight **Asian clusters** (dumplings–ramen–hotpot), **BBQ–fried chicken** synergy; **sushi** acts as a **bridge** across clusters.&#x20;
* **Restaurant Segments (K=4):** budget, mid-range/popular, high-end/loyalty, niche/specialty.&#x20;
* **Forecasting:** LSTM/Prophet indicate **2016 momentum** skewed to **healthy + global** (e.g., tofu, matcha, hummus, spinach), alongside **indulgent desserts & premium beverages**.&#x20;
* **Validation:** Google Trends & brand comps (e.g., Chipotle growth) **corroborate taco acceleration** vs slower sushi.&#x20;

---

## 🧭 Business Impact (Examples)

* **Menu & Promo Design:** bundle **co-occurring items** (e.g., dumplings+ramen) and time promos with **seasonal peaks** (winter comfort foods).&#x20;
* **Product & Launch:** invest in **rising global categories** (Mexican/Asian) and **better-for-you** ingredients.&#x20;
* **Inventory Planning:** align **ingredient orders** (e.g., chicken, cheese, pork, shrimp) with forecasted dish cycles.&#x20;
* **Location Strategy:** target **neighborhoods** with favorable **healthiness/trend indices** for concepts and merchandising.&#x20;

---

## ⚠️ Limitations

* **Geography & timeframe:** Philadelphia only; 2013–2016 window.&#x20;
* **Data proxies:** review mentions ≠ exact orders; potential sampling bias.
* **Seasonality/noise:** strong seasonality and event spikes increase variance.
* **Engineering constraints:** model performance varies by item; beverages forecast best; dataset and collaboration frictions noted.&#x20;

---

## 📁 Files Included

* `K-Means Clustering & Co-occurrence Network Analysis.ipynb`
  Clusters restaurants (K-Means), builds **dish co-occurrence** graphs, and extracts cross-sell candidates.
* `Keyword Frequency Analysis.ipynb`
  Monthly **frequency & seasonality** trends for dishes/cuisines.
* `final_ner.ipynb`
  **Named Entity Recognition** to extract dish/cuisine mentions for ranking over time.
* `TopicModeling.ipynb`
  **LDA** with 12 topics; absolute/relative topic-share changes (2013–2015).
* `final_tsa.ipynb`
  Classical **time-series analysis** baselines (decomposition/Prophet).
* `FinalLSTM_Model.ipynb`
  **Deep learning** forecasting of dish trajectories; item-level **MAE** comparison.
* `Predicting Emerging Food Trends.pptx`
  Executive summary, visuals, validation exhibits, and business recommendations.&#x20;
---

## ▶️ How to Run

1. **Environment**

   * Python 3.10+
   * `pandas numpy scikit-learn nltk spacy gensim networkx matplotlib plotly prophet tensorflow keras`
   * Models may require installing language models (e.g., `python -m spacy download en_core_web_sm`).

2. **Data**

   * Place merged **Philadelphia restaurant reviews** CSV in `data/` (not included due to size/licensing).
   * Expected columns include: business metadata, review text, useful/stars, year/month.

3. **Execution Order (suggested)**

   1. `Keyword Frequency Analysis.ipynb`
   2. `final_ner.ipynb`
   3. `TopicModeling.ipynb`
   4. `K-Means Clustering & Co-occurrence Network Analysis.ipynb`
   5. `final_tsa.ipynb`
   6. `FinalLSTM_Model.ipynb`

4. **Reproducibility**

   * Set random seeds where available (`numpy`, `tensorflow`).
   * Save intermediate tables to `outputs/` for reuse across notebooks.

---

## 📊 Outputs You Can Expect

* Ranked lists of **rising/declining dishes** by YoY change.
* **Seasonal calendars** for key categories.
* **Co-occurrence networks** for combo design.
* **Cluster labels** for restaurants.
* **Forecast plots** + **MAE tables** by item.
* **Validation panels** vs Google Trends/brand comps.&#x20;

---

## 📌 Roadmap / Future Work

* Broaden to **additional cities/states**; federated learning for multi-tenant clients.
* **Causal drivers** (price, weather, events) and **hierarchical forecasts** (dish→cuisine→category).
* **Menu generator** and **supplier order recommender** built on forecasted demand.&#x20;

---



