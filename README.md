# Predicting Patient Show/No Show

In this project I forecasted likelihood of patient show/no show for an appointment using patient EHRs, resulting in an increase in prediction accuracy from 0.81 (baseline) to 0.91. 
This model empowers providers to take the actions necessary to reduce cost and improve patient outcomes by ensuring high risk patients attend appointments.

## Getting Started

Download the data set from [Kaggle](https://www.kaggle.com/joniarroba/noshowappointments) OR from this repo

## Approach
### White Paper
Rea the complete white paper [here](https://docs.google.com/document/d/11Nhi-5B-3z3fbnh5Tf0kzD4D-IbvRZCCVwjBcTYghS4/edit?usp=sharing)

### 1. Literature Review
Prior to beginning this project a literature review was conducted to ensure understanding of the problem space, and to facilitate feature and model selection. From the literature review it was understood that patient no-show is a huge burden on the healthcare system (costing an estimated $150billion per year). Predicting patients likely to miss their appointments accurately can empower healthcare providers to take the action necessary to reduce no-show costs and improve patient outcomes. From the literature common features were identified and added to the model including: WaitTime, NoShowRatio, DayWeek, DayMonth. In addition to features, candidate classification models were identified including: Support Vector Machine, Logistic Regression, Naive Bayes. 

### 2. Data Cleaning
The original dataset contained the following features: PatientId, AppointmentID, Gender, ScheduledDay, AppointmentDay, Age, Neighbourhood, Scholarship, Hipertension, Diabetes, Alcoholism, Handcap, SMS_received, No-show. These features were removed of typos and converted into their appropriate data types. Non-numerical features such as Gender, Neighbourhood, and NoShow were converted into numerical features by encoding.
It is noteable that the dataset consisted of roughly 80% No instances and 20% Yes instances. This means that a baseline prediction of all “No” could achieve an accuracy of ~80%. 

### 3. Feature Exploration & construction
To explore the features histograms and count plots were used. As a result of this feature exploration the following features were earmarked for further investigation: Diabetes, Alcoholism, Hypertension due to their strong relationship with our target variable.
We then chose to construct five new features: NumAppts, SumNoShow, NoShowRatio, DayWeek, DayMonth.

### 4. Model Selection  
To solve this problem five models were implemented and the results compared. Each model was computed using 10-fold cross validation to reduce overfitting. The following models were selected because they are well suited for binary classification. The models used include:
  * Logistic Regression 
  * Linear Discriminant Analysis
  * K Neighbors Classifier
  * Decision Tree Classifier
  * Gaussian Naive Bayes

We then took the model with the highest training accuracy, Logistic Regression, and implemented a train/test split of 70/30 to train the model that would generate our submission output.

### 5. Feature Selection 
For our final model recursive feature elimination (RFE) was performed, recursively pruning the set of candidate features to yield the most significant features. The top 7 features, all ranked #1, were incorporated in the final model to generate the submission file (predictions for a given test set).

## Assumptions
When creating features it was assumed that a patient's history of missing appointments would be highly indicative of missing future appointments, so the following features were constructed: NumAppts, SumNoShow and NoShowRatio. This assumption was supported by Dr. Carly’s talk in class on April 7, 2018 on Prediction of Patient No-Shows.

## Limitations
If I were to reconduct this experiment I would conduct the following changes: 
* Due to the highly unbalanced class labels (80% yes, 20% no) I would experiment with varying threshold values for the logistic regression classification rather than just using the standard 0.5.
* Because the data contains features that range in value in quite a large manner, I would also try normalizing the features and see if that changes my results. 
* Although 10 fold CV was performed to reduce overfitting, I would be interested to see how this model generalizes on an unseen validation data set.

## Acknowledgments
Thank you to Dr. Ankur Teredesai, Dr. Muhammad Ahmad and Dr. Carly Eckert for their guidance in completing this project. 
