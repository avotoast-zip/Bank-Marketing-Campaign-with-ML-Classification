<h1> Bank Marketing Campaign with Machine Learning Classification </h1>

## 1. Project Overview
A Portuguese banking institution conducted a telemarketing campaign to promote its term deposit product. The main goal of this campaign was to identify whether a customer would subscribe to the term deposit after being contacted. Information collected during the campaign includes demographic data, socio-economic status, and interaction details from current and previous campaigns.

**Target:**
- **0**: The customer did not subscribe to the term deposit (`y = "no"`)
- **1**: The customer subscribed to the term deposit (`y = "yes"`)

## 2. Problem Statement
Telemarketing campaigns are expensive and time-consuming, especially if conducted without targeting. The bank aims to build a system that can predict the likelihood of a customer subscribing to the term deposit, so they can focus efforts on the most promising leads.

If a call is made to a customer who is unlikely to subscribe, it wastes time and money. On the other hand, if a potential customer is not contacted, it results in a missed opportunity.

## 3. Goals
Based on the problem above, the goals are:
- Predict whether a customer will subscribe to a term deposit or not.
- Identify the most influential factors/variables that drive a customer to subscribe.

## 4. Analytic Approach
- Analyze historical marketing data to find patterns in customer behavior related to subscription.
- Build a classification model (e.g., Logistic Regression, Decision Tree, Random Forest, etc.) to predict the likelihood of a customer subscribing.

## 5. Metric Evaluation

- **Type 1 Error (False Positive):** Predicting that a customer will subscribe when they actually won’t.  
  **Consequence:** Wasted campaign time and cost.

- **Type 2 Error (False Negative):** Predicting that a customer will not subscribe when they actually would.  
  **Consequence:** Missed opportunity to acquire a customer.

Given the consequences, the goal is to:
- Maximize true positive predictions,
- Minimize false positives without losing too many true positives.

**Primary metric to use**: `roc_auc` and `recall` on the positive class.

---
## 6. Data Sources
**Dataset source**: [UCI Machine Learning Repository](https://archive.ics.uci.edu/ml/datasets/Bank+Marketing)

## 7. Technologies Used
- Programming Language: Python
- Visualization: Matplotlib, Seaborn, Plotly
- ML: Scikitlearn, Imblearn
- Version Control: Git
- Others: Jupyter Notebook

## 8. Project Structure

```
├── README.md          <- The top-level README for developers using this project.
├── data
│   ├── external       <- Data from third party sources.
│   ├── interim        <- Intermediate data that has been transformed.
│   ├── processed      <- The final, canonical data sets for modeling.
│   └── raw            <- The original, immutable data dump.
│
├── models             <- Trained and serialized models, model predictions, or model summaries
│
├── notebooks          <- Jupyter notebooks. Naming convention is a number (for ordering),
│                         the creator's initials, and a short `-` delimited description, e.g.
│                         `1.0-jqp-initial-data-exploration`.
│
├── references         <- Data dictionaries, manuals, and all other explanatory materials.
│
├── reports            <- Generated analysis as HTML, PDF, LaTeX, etc.
│   └── figures        <- Generated graphics and figures to be used in reporting
│
├── requirements.txt   <- The requirements file for reproducing the analysis environment, e.g.
│                         generated with `pip freeze > requirements.txt`
│
└── src                <- Source code for use in this project.

```

## 9. Summary of Finding
### 5.1 Business Insight
In conclusion, our model can correctly predict when a customer would not be interested in placing a term deposit (so as to skip approaching them) 88% of the time, and predict 60% out of all actually interested candidates. We know this from the recall score.

Our model is 40% precise in predicting interest in opening a term deposit.

Although direct figures for marketing costs in Portugal are unavailable, we can consider general benchmarks:
- Telemarketing Costs: In various markets, the cost of a telemarketing call can range from €0.50 to €2.00, depending on factors like call duration and labor costs. We will take the average, which is €1.25
- Conversion Rates: With an 11% success rate, as observed in the Portuguese dataset, approximately 9 calls are needed for one successful subscription.

Using these estimates:

At €1.25 per call: €1.25 × 9 = €11.25 per customer.

So, for 100 potential customers, with 50 actually interested customer:

1. Without model (all potential customers contacted)
    - Telemarketing Cost: €11.25 x 100 = €1125
    - Total Interested Candidates Acquired: 50 (assumed to all be contacted)
    - Total Interested Candidates Missed: 0
    - Wasted Cost: 50 uninterested × €11.25 = €562.50
    - Total Cost: €1,125
    - Savings: €0 (baseline)

2. With model
Model Recall (for class 1 / interested): 60% → out of 50 actually interested candidates, model correctly identifies 30
Model Precision (for class 1 / interested): 40% → to get 30 correct, model predicts interest in 75 people
    - Telemarketing Cost: €11.25 × 75 = €843.75
    - Total Interested Candidates Acquired: 30
    - Total Interested Candidates Missed: 50 - 30 = 20
    - Wasted Cost: 45 uninterested × €11.25 = €506.25
    - Total Cost: €843.75
    - Savings: €281.25

### 5.2 Actionable Recommendation
- Explore additional features that could influence customer behavior. While the current dataset is clean and well-structured, the model could benefit from incorporating new attributes—such as a customer's existing financial products, account activity levels, preferred communication channels, or even recent transaction patterns. These could provide a more complete picture of a customer’s financial engagement and potential interest.

- Experiment with different machine learning algorithms and resampling techniques. Beyond the models already tested, it would be valuable to assess the performance of other classifiers (e.g., XGBoost, CatBoost, or ensemble methods) and apply more advanced oversampling strategies such as SMOTENC or ADASYN, particularly given the imbalanced nature of the target variable.

- Fine-tune hyperparameters with a more robust search strategy. While some tuning has been done, using techniques like randomized search or Bayesian optimization across a broader parameter space might yield even better-performing models.

- Investigate cases where the model makes incorrect predictions. Specifically, analyzing false negatives (interested customers missed by the model) and false positives (disinterested customers wrongly targeted) can uncover behavioral patterns or subgroups that are not yet well captured by the features. These insights could guide future feature engineering or segmentation strategies.

## 10. Contact
- Name: Cindy H. Tantowibowo
- Email: cindyhtantowibowo@gmail.com
- Linkedin: Cindy Handoko Tantowibowo
