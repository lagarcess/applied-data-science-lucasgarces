# PowerCo Customer Churn Analysis: Investigating Price Sensitivity

## 1. Background & Problem Statement

**Client:** PowerCo is a major gas and electricity utility supplying to small and medium-sized enterprises (SMEs).

**Context:**

> The energy market has become increasingly competitive in recent years, presenting customers with more provider options than ever. Consequently, PowerCo is experiencing a significant problem with customer churn—customers leaving for better offers from competitors. This trend poses a substantial risk to their revenue and market share.

**Core Hypothesis:**

> The primary hypothesis from the client is that this churn is driven by customers becoming more price sensitive. They believe customers are actively seeking and switching to lower-cost alternatives.

**Price Sensitivity Definition:**

> For this project, price sensitivity is defined as the degree to which customer behavior (specifically, the decision to churn) changes in response to a change in price. Our goal is to quantify this effect and determine its significance as a driver of churn.

---

## 2. Project Scope

The objective of this project is to validate or disprove the hypothesis that price sensitivity is the critical factor driving customer churn at PowerCo.

### In Scope

- **Analyze Historical Data:** Utilize the provided customer and pricing datasets to understand past behavior.
- **Establish Causality:** Move beyond correlation to determine the direct causal impact of price increases on a customer's decision to churn.
- **Build Predictive Models:** Develop models to identify which customers are most likely to churn and when, enabling proactive retention efforts.
- **Deliver Actionable Insights:** Provide a clear profile of the most price-sensitive customer segments and offer data-driven recommendations for PowerCo's pricing and retention strategies.

### Out of Scope

- Collection of new or external market data.
- In-depth analysis of non-price-related churn drivers (e.g., customer service quality, service diversity), unless directly available in the provided data.
- Development and deployment of a real-time production model.

---

## 3. Plan of Action

Our analysis will follow a structured **5-step data science workflow** to ensure a comprehensive and robust investigation.

### Step 1: Understand and Frame the Business Problem

**Status:** Complete

> We have framed the core problem: SME customers are churning, and we must test the hypothesis that price sensitivity is the critical factor.

### Step 2: Exploratory Data Analysis (EDA)

**Action:** This is our exploration and diagnosis phase. We will validate the problem and uncover initial patterns by:

- Analyzing the overall churn rate over time
- Segmenting churn by business type, sales channel, and consumption levels
- Visually correlating price changes with churn events

### Step 3: Feature Engineering

**Action:** We will create new, powerful features from the raw data to improve model performance, including:

- `customer_tenure`
- `treatment_price_hike` (a binary or continuous variable indicating a significant price increase)
- `price_volatility` and `time_since_last_price_increase`
- `energy_consumption_volatility`

### Step 4: Modeling and Evaluation

**Action:** This is where we move from correlation to causation and prediction, using a multi-faceted modeling approach:

#### Establish Causality (Updated Approach)

- **Difference-in-Differences (DiD) with Propensity Score Matching (PSM):**
  - Create a robust control group by matching customers who received a price hike with similar customers who did not.
  - Use DiD to get a clear, interpretable estimate of the average causal effect of a price increase.
- **Causal Forests:**
  - Train a Causal Forest model to estimate the treatment effect for individual customers, identifying which specific segments are most sensitive to price changes.
- **Predict Who Will Churn:**
  - Build a Logistic Regression model to calculate a churn probability score for each customer.
- **Predict When They Will Churn:**
  - Use Survival Analysis to forecast the timing of churn, enabling precisely timed retention strategies.

### Step 5: Insights and Recommendations

**Action:** Finally, we will synthesize all findings into a clear, non-technical narrative for the client. The deliverables will be:

- A definitive, data-backed answer on the causal impact of price on churn
- A clear profile of the most price-sensitive customer segments
- A framework for a predictive tool to help PowerCo proactively identify and retain at-risk customers
