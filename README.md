# Predicting Heart Attack Risk #
Heart disease is a leading cause of death in regions in India, yet many high-risk individuals go undetected until it’s too late. This analysis builds a predictive model to identify key risk factors for heart attacks, leveraging machine learning and public health data to improve early detection and inform targeted prevention strategies.

![Ministry of Health & Family Welfare - India](mofhw_image.png)

### Business Understanding ###
The dataset is based on Indian cardiovascular health statistics, medical research reports, and national surveys, incorporating data from:

Indian Council of Medical Research (ICMR) – Reports on heart disease prevalence in India Ministry of Health & Family Welfare, Government of India – National health statistics World Health Organization (WHO) – India Reports – Cardiovascular disease risk factors National Family Health Survey (NFHS-5) – Demographic and health-related indicators Global Burden of Disease (GBD) Study – India-specific cardiovascular mortality rates Indian Heart Journal & AIIMS Research – Clinical insights on CVD trends in India.

This dataset consists of 10,000 records with each corresponding to a patient ID and their associated health characteristics, conditions, lifestyle choices and other related metrics culminating in assessing whether or not the patient is at risk for a heart attack. We also have no null values in our dataset.

### Data Understanding ###
Our target variable is imbalanced (with roughly a 70/30 split). We will prepare our data to handle this class imbalance and then proceed with random under sampling on a logistic regression model.

In order to prepare our data for analysis we must do the following steps. We will drop any non-informative columns such as patient ID, state name and emergency response time and then assign heart attack risk as our target variable. We'll also label encode gender to be binary with female being 0 and male being 1. After we'll split our data using train test split with training making up 70% and test data making up 30%. We'll then have to standard scale our numeric columns (non-binary) to make other features on the same evaluation scale for analysis.

### Baseline Model & Evaluation ###
We'll establish a starting point for evaluating heart attack risk through an initial logistic regression model. Logistic regression is widely used because it is simple and interpretable. This is an ideal first model for our binary classification analysis.

Accuracy is around 70% but a major limitation is that it is never predicting class 1 (high risk of heart attack cases). Precision, recall and F1-score for this class is 0.

Our model is classifying every test sample as low risk which makes it useless for public health decision-making. While our target class is not extremely unbalanced, logistic regression is still favoring the majority class.

We have 469 correctly predicted high-risk cases, 419 correctly predicted low-risk cases, 484 wrongly predicted high-risk cases that were actually low-risk, and 433 wrongly predicted low-risk cases that were actually high-risk.

We will proceed with random undersampling our model in hopes to yield better results from a more balanced class.

### Random Undersampled Model & Evaluation ###
Since our dataset is imbalanced in the target class we'll iterate on our baseline logistic regression model with random under sampling. The imbalance caused our model to favor predicting class 0 (low-risk patients). Random undersampling balances the dataset by reducing the number of the majority class and ensures our model learns patterns from both classes equally.

This is slightly worse than random guessing (50%) which means that the model struggles to find meaningful patterns after undersampling.

However, our model is now at least predicting both class 0 and 1. Our model had 419 true negatives (correctly predicted no heart attack risk), 433 false negatives of high-risk patients misclassified as low-risk, 484 false positives of low-risk patients wrongly classified as high-risk, and 469 true positives of correctly predicted high-risk patients.

Our recall was 0.46 for class 0 and 0.52 for class 1. For class 1, recall of 0.52 means that the model misses 48% of actual heart attack cases (false negatives).

Precision was 0.49 for both classes, meaning the model isn't precise in predicting correct positives. This leads to many false positives.

F1-score was 0.49 for both classes, meaning the balance between recall and precision isn't that great. Our model isn't very useful for making predictions yet.

### Decision Tree Model & Evaluation ###
We will iterate upon our undersampled model rather than our baseline model because it yielded a better F1-score. We will next use a decision tree model because it provides clear, interpretable rules for risk assessment and captures more complext relationships between our medical, socioeconomic and behavioral factors. F1-score is vital to build off of because it provides us information on creating a healthy balance of cases we predicted as high-risk actually being high-risk and cases of actual high-risk that were correctly identified as high-risk. Accuracy alone is misleading in imbalanced datasets.

We'll proceed with a decision tree classifier model to account for an extra layer of complexity among our features. The decision tree will make predictions by splitting data into branches based on feature values.

Our accuracy improved slightly from our undersampled evaluation to 50%. Our decision tree also predicted both class 0 and 1 pretty evenly. We had 431 false positives, meaning many low-risk individuals are misclassified as high-risk. We also had 454 false negatives of actual high-risk patients that are missed.

Our model isn't very precise at 0.50 for both classes, meaning if the model predicts someone is at risk of a heart attack it's only correct 50% of the time. Our recall also sits at 0.49 for class 1, meaning it only detects about half of the actual high-risk patients. Our F1-score remained roughly the same as our undersampled evaluation. This still reflects poor balance between both precision and recall.

### Conclusion ###
These charts show the magnitude of importance/impact each feature has on heart attack risk. The decision tree model suggests that annual income and biological measures such as triglyceride level, LDL level and systolic BP are major predictors of heart attack outcomes. Our logistic regression model suggests that diabetes, smoking and alcohol consumption are strong contributors to heart attack.

Given that the MoHFW aims to develop public health strategies to prevent heart attacks, I'd recommend pursuing public health initiatives based on findings from our decision tree model. Our decision tree model captures non-linear relationships (as opposed to our linear regression model that assumes simple linear relationships between features and heart attack risk) and highlights larger scale public health policy and resource allocation.

Low-income populations was the biggest predictor for heart attack risk from our decision tree model but a limitation of this dataset is that we don't know what the binary 0 and 1 means in terms of socioeconomic tier. To better support this as a major indicator to heart attack risk, it'd be helpful to gather additional data to know the patient's health insurance type and coverage level, out-of-pocket healthcare costs, and employment type/income tiers. With more flushed out socioeconomic and healthcare data, we can move from broad public health suggestions to targeted, evidence-based policy interventions.

### Repository Navigation ###

[View Presentation on Google Slides](https://docs.google.com/presentation/d/1RsxMgCRa7LfmHMT9YG2YNTu4p7qFwAQr-dlwW8AONHM/edit#slide=id.p)
[Jupyter Notebook](Heart Attack Analysis.ipynb)
