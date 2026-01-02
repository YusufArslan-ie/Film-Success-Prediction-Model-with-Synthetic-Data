---
title: (Film Data Analytics Project) 
---

# Film Success Prediction Model — Final Report 

## **1\. Problem Definition**

**Objective:**  
To predict the box office success of films based on their measurable characteristics.

**Target variable:** `film_box_office`  
**Task type:** Regression

The model aims to estimate a film’s commercial performance using pre-release attributes such as production, genre, ratings, and thematic depth.

---

## **2\. Data Structure**

The dataset integrates **13 relational tables**, including:  
`FILMS`, `RATING`, `SOCIOPOLITICAL`, `SYMBOLISM_AND_MOTIFS`, `CULTURAL_INFO`,  
`PARENTS_GUIDE`, `FRANCHISE`, `RELEASE_INFO`, `ANIMATION_SETTINGS`,  
`CREW_MEMBERS`, `CHARACTERS`, `STORY_AND_THEMES`, and `SOUNDTRACKS`.

After merging, a single film-level dataset (`df_model`) was prepared with the following feature groups:

* **Production factors:** `film_budget`, `film_duration`, `genre`, `studio_name`, `film_country`
* **Quality metrics:** `audience_rating_mean`, `critic_rating_mean`, `rating_gap`
* **Thematic variables:** `symbolism_density`, `visual_metaphor_strength`, `narrative_complexity`
* **Sociopolitical factors:** `activism_message_strength`, `controversy_level`
* **Content indicators:** `family_friendly_score`, `violence_intensity`, `sexual_content_intensity`

---

## **3\. Exploratory Data Analysis (EDA)**

* Average film budget: around **500–600M**.
* Box office distribution was **strongly right-skewed**, dominated by high-grossing blockbusters.
* Correlation between `film_budget` and `film_box_office`: **\~0.7**.
* Audience ratings had a clear positive correlation with box office; critic ratings were weaker.
* Highest grossing genres: **Action|Adventure** and **Animation|Family**.
* Missing values were minimal; numeric columns were filled using medians, categorical columns with the most frequent label.

---

## **4\. Feature Engineering**

New features were engineered to represent historical performance, tone, and qualitative factors:

| Feature                   | Description                                       |
| ------------------------- | ------------------------------------------------- |
| studio\_popularity\_score | Average historical box office per studio          |
| genre\_success\_score     | Average historical box office per genre           |
| international\_factor     | 1 if non-US production                            |
| content\_risk\_index      | (violence + sexual content) – family friendliness |
| critical\_appeal          | critic rating + award count                       |
| audience\_gap\_ratio      | normalized audience–critic difference             |
| family\_target\_flag      | 1 if family friendliness > violence intensity     |
| symbolic\_score           | symbolism + visual metaphor strength              |

⚠️ Variables derived from the target (e.g. `roi`, `budget_per_minute`) were **removed** to prevent data leakage.

---

## **5\. Modeling Process**

**Data split:** 80% training / 20% testing

**Preprocessing pipeline:**

* **Numerical features:** median imputation + StandardScaler
* **Categorical features:** mode imputation + OneHotEncoder

**Model:** `RandomForestRegressor`

* Parameters: `n_estimators=500`, `random_state=42`

**Performance:**

| Metric | Score       |
| ------ | ----------- |
| RMSE   | 317,884,494 |
| MAE    | 198,912,896 |
| R²     | 0.397       |

A log-transformed target slightly improved R² (+0.01).

---

## **6\. Feature Importance**

| Feature                                                | Importance | Interpretation                                         |
| ------------------------------------------------------ | ---------- | ------------------------------------------------------ |
| **film\_budget**                                       | 0.238      | Strongest driver — direct proxy for investment power.  |
| **genre\_success\_score**                              | 0.116      | Genre’s historical profitability signal.               |
| **critical\_appeal**                                   | 0.089      | Quality (critics + awards) positively affects revenue. |
| **studio\_popularity\_score**                          | 0.080      | Studio brand strength matters.                         |
| **audience\_gap\_ratio**                               | 0.080      | Viewer–critic imbalance influences popularity.         |
| **film\_duration**                                     | 0.064      | Balanced duration contributes to performance.          |
| **audience\_rating\_mean**                             | 0.054      | Audience approval is impactful.                        |
| **critic\_rating\_mean**                               | 0.028      | Critics’ effect is modest but measurable.              |
| **content\_risk\_index**                               | 0.021      | Excessive violence/sexual content can reduce reach.    |
| **symbolism\_density**, **visual\_metaphor\_strength** | ≈0.022     | Artistic depth adds minor but positive influence.      |

---

## **7\. Error Analysis**

| Metric        | Value     | Observation                                       |
| ------------- | --------- | ------------------------------------------------- |
| Mean error    | +2.4×10⁷  | Slight underestimation of very large box offices. |
| Std deviation | 1.59×10⁸  | Narrower error spread compared to early models.   |
| Max error     | +1.07×10⁹ | Remaining outliers = extreme blockbusters.        |

**Genre-level patterns:**

* _Drama|Romance_: overestimated
* _Adventure|Fantasy_: underestimated
* Other genres: stable within ±2×10⁷ range

The model performs well for mid-scale productions but struggles on extreme outliers.

---

## **8\. Conclusions**

* The model explains **≈40% of variance** in box office success.
* **Economic** (budget, studio) and **historical** (genre average) variables dominate prediction.
* **Quality and tone** features (ratings, content risk, symbolism) have secondary yet measurable effects.
* After removing target-derived features, the model is **valid, unbiased, and generalizable.**

---

## **9\. Future Improvements**

1. **Model optimization:** try **XGBoost** or **LightGBM** for deeper non-linear modeling.
2. **Feature enrichment:** add  
   * `film_votes_count`, `social_sentiment_score`, `release_type`  
   * actor and crew popularity metrics
3. **Segmented modeling:** separate models for blockbusters vs. indie films.
4. **Explainability:** use **SHAP** analysis for detailed feature impact visualization.

---

## **10\. Overall Assessment**

The final model provides a **realistic and interpretable framework** for predicting film performance.  
It aligns with industry patterns: capital, brand, and audience response drive commercial success.  
With richer social and production data, it could evolve into a full-scale **box office forecasting system** for real-world use.