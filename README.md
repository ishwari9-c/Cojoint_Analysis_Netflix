# 🎬 Netflix Subscription Conjoint Analysis 

![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)
![Statsmodels](https://img.shields.io/badge/Library-Statsmodels-orange.svg)
![Data Analysis](https://img.shields.io/badge/Data%20Analysis-Conjoint-success.svg)

## 📌 Project Overview
This project applies **Choice-Based Conjoint Analysis (CBC)** to simulate how consumers make complex trade-offs regarding streaming service subscriptions. By analyzing customer survey data, this project quantifies the perceived value (part-worth utilities) of various Netflix subscription features, helping to understand what drives user purchasing decisions and retention.

## 🎯 Business Problem
Streaming platforms face high churn rates and complex pricing tiers. To maximize revenue, a platform must understand the trade-offs consumers are willing to make:
* How much does price actually impact the decision compared to account sharing?
* Are users willing to accept ads if premium content (like HBO or Disney) is included?
* What is the threshold where a high price causes a severe drop in user interest?

## 📊 The Data
* **Dataset:** `data/netflix_customer_survey.csv` (3,000 customer survey responses)
* **Attributes Analyzed:**
  * **Number of Accounts:** 1, 2, 3, 4, 5, 6
  * **Price:** $8, $10, $12, $15, $18, $20
  * **Extra Content:** Disney, HBO, Marvel, Prime originals, Soccer, less content
  * **Ads:** None, one_per_day, one_per_show

## 🛠️ Methodology & Tech Stack
* **Language:** Python
* **Libraries:** Pandas, NumPy, Statsmodels, Matplotlib, Squarify
* **Techniques:** 
  * Dummy variable encoding for categorical attributes.
  * **Generalized Linear Models (GLM - Binomial Family)** to run logistic regression.
  * Calculation of **Part-Worth Utilities** to measure individual feature level preferences.
  * **Relative Feature Importance** derivation using max-min part-worth ranges.
  * **Interaction Terms** to study the combined effect of Content and Ad frequency.

## 💡 Key Findings & Insights

### 1. Relative Feature Importance
Contrary to the assumption that price dictates all streaming choices, **Number of Accounts** was the most influential factor in the user's decision-making process, driving 33.9% of the decision weight.
* **Number of Accounts:** 33.9%
* **Price:** 27.6%
* **Extra Content:** 22.4%
* **Ads:** 16.1%

![Relative Importance](images/relative_importance_treemap.png)

### 2. Part-Worth Utilities (Main Effects)
* **The Single Account Penalty:** Restricting users to exactly 1 account had the single most negative impact on perceived value (part-worth: -0.70). Offering 6 accounts was highly valued (0.49).
* **Price Thresholds:** Users showed positive utility for price points up to $12. However, a $20 price point resulted in a massive drop in preference (-0.68 part-worth).
* **Content Preferences:** "Disney" and "HBO" add-ons drove the highest positive utility (0.227 and 0.226, respectively), while "less content" severely hurt the offering (-0.56).

![Part-Worth Utilities](images/percived_value_customer.png)

### 3. Interaction Effects (Content vs. Ads)
By creating interaction terms between `ExtraContent` and `ads`, the model revealed nuanced customer tolerances:
* **The Ideal Bundle:** The combinations of `Disney_one_per_day` (0.547) and `HBO_none` (0.529) generated the highest overall perceived value.
* **Ad-Tolerance:** Interestingly, users highly valued the Disney package *even with one ad per day*, suggesting that premium content can successfully offset mild ad intrusions.
* **The Worst Bundle:** Combining "less content" with "one ad per show" resulted in a devastatingly low utility score (-1.09).

![Interaction Terms](images/interaction_terms.png)

## 🚀 How to Run the Project

1. **Clone the repository:**
   ```bash
   git clone [https://github.com/Prathameshkate15/Netflix_Conjoint_Analysis.git](https://github.com/Prathameshkate15/Netflix_Conjoint_Analysis.git)
   cd Netflix_Conjoint_Analysis