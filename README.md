# Fraud-Detection-Analysis

## Project Overview:

This project aims to enhance the accuracy of detecting fraud in mobile financial transactions. By leveraging machine learning, the project seeks to predict fraudulent transactions with high precision. The goal is to develop a robust machine learning model to accurately identify fraudulent transactions in real-time , enabling the company to improve security, reduce financial losses, and gain insights into factors contributing to transaction fraud.
 
## Deliverables: 

A production-ready machine learning model for fraud detection. 
Comprehensive analysis of model performance and expected financial impact. 

Dataset : Fraud_Analysis_Dataset.csv

---

## Data Overview:

### Dataset:
<img width="1291" height="258" alt="image" src="https://github.com/user-attachments/assets/ed7bdfb7-33e3-4ea5-abc0-73ce8cb62969" />

### Description:
<img width="973" height="652" alt="image" src="https://github.com/user-attachments/assets/2c008b63-c05e-4b32-b105-6eae239be864" />

---

## Exploratory Data Analysis:

For our **Exploratory Data Analysis (EDA)**, we'll take it in two main steps:

**1. Univariate Analysis:** Here, we'll focus on one feature at a time to understand its distribution and range.

**2. Bivariate Analysis:** In this step, we'll explore the relationship between each feature and the target variable. This helps us figure out the importance and influence of each feature on the target outcome.

With these two steps, we aim to gain insights into the individual characteristics of the data and also how each feature relates to our main goal: predicting the target variable.

**Numerical Features :** step, amount, oldbalanceOrg, newbalanceOrig, oldbalanceDest, newbalanceDest

**Categorical Features :** type

**Target :** isFraud

### 1. Numerical Feature Univariate Analysis:

**Time (`step`) :** Right skewed distribution, Average time of transaction is 13 hours

**Transaction Amount (`amount`):**  The graph shows that most transactions are for small amounts, average transaction of 400k

**Sender's Transaction (`oldbalanceOrg` & `newbalanceOrig`):** The distributions are highly concentrated near zero, which is expected since many transactions, especially for a large customer base, would involve small balances. The extremely high outliers are strong indicators of potential fraud. A sudden, massive change in balance or a transaction involving an unusually large account balance could be a key sign of an account takeover or other fraudulent activity.

**Receiver's Transaction (`oldbalanceDest` & `newbalanceDest`):** Similar to the source balances, the distributions are also heavily right-skewed and have significant outliers. A large amount being transferred into or out of an account with a previously low or zero balance, especially for a destination account that is not a known customer, could be a strong signal of fraudulent activity.

<img width="1000" height="993" alt="image" src="https://github.com/user-attachments/assets/babb4932-858a-4d1d-b922-8efa7f4c6803" />

### 2. Categorical Feature Univariate Analysis:

**Transaction Type (`type`):** The plot shows that CASH_IN (34.6%) and CASH_OUT (33.2%) are the most frequent transaction types, together accounting for over two-thirds of all transactions. TRANSFER (26.0%) is also a significant type, while DEBIT (6.1%) is relatively rare.

**No. of Fraud (`isFraud`):**  A massive 79.7% of transactions are legitimate (isFraud = 0), while only 20.3% are fraudulent (isFraud = 1).

<img width="985" height="718" alt="image" src="https://github.com/user-attachments/assets/0c45d6f8-9379-4cec-aab0-58922d07514a" />

### 3. Numerical Feature Bivariate Analysis:

The Bivariate Analysis of continuous features against the isFraud target reveals highly actionable insights. The distributions of fraudulent and non-fraudulent transactions are remarkably different across all variables.

The most powerful fraud signals are:

 **1. Time:** Fraudulent transactions occur later in the dataset (step).
 
 **2. Amount:** They involve significantly higher transaction amounts.
 
 **3. Balance Discrepancies:** They are characterized by a drastic reduction in the source account's balance (oldbalanceOrig to newbalanceOrig) and a substantial increase in the destination account's balance from a low starting point (oldbalanceDest to newbalanceDest).

<img width="1000" height="1114" alt="image" src="https://github.com/user-attachments/assets/053011c1-7696-4a87-974b-2d4c6d5f8621" />

### 4. Categorical Feature Bivariate Analysis:

**CASH_IN  have 0% Fraud:** The most significant finding is that CASH_IN  transaction types have zero fraudulent cases in the dataset. 

**DEBIT also has 0% Fraud:** The DEBIT transaction type, which represents a small portion of the overall transactions, also shows zero fraud.

**CASH_OUT and TRANSFER are associated with Fraud:** In stark contrast, CASH_OUT and TRANSFER transactions are where all fraudulent activity is concentrated.

* CASH_OUT : transactions have a fraud rate of 30.9% (578 out of 1,871).
* TRANSFER: transactions have the highest fraud rate at 38.5%(564 out of 1,464).

<img width="764" height="615" alt="image" src="https://github.com/user-attachments/assets/d2f9f77f-fddb-4590-ab39-cb454c723307" />

### 5. Multivariate Analysis:

* High Positive Correlation on Target: `Amount`
* Moderate Positive Correlation on Target: `Old Balance Origin`
* High Negative Correlation on Target: `New Balance Origin`
* Moderate Negative Correlation on Target: `Old Balance Destination`
* Less Correlation on Target: `New Balance Destination`

Target = ‘isFraud’

<img width="938" height="858" alt="image" src="https://github.com/user-attachments/assets/30253ce2-7df8-4540-8377-85710a7f5d9d" />

---

## Data Preprocessing:

### Preprocessing:

* **Irrelevant Feature Removal :** Features such as ‘nameOrg’ & ‘nameDest’ found to be irrelevant, hence removed.
* **Missing Value Treatment :** No missing values are found in the dataset
* **Outlier Treatment :** Checked outliers using IQR method for the continuous features and upon identifying outliers, nature of algorithm, and given small dataset size direct removal of outliers might not be best approach. Instead, we will apply Box-Cox transformation to stabilize variance and make the data more normal-distribution.
* **Categorical Features Encoding :** Applied One Hot Encoding on ‘type’, since it is a nominal variable.
* **Feature Scaling :** Are imp. for the algorithms that are sensitive to the magnitude and scale of feature, but not all algorithms requires scaling like Decision Tree are scale-invariant and given our intent to use mix-model we’ve chosen to handle scaling later using pipelines.

### Feature Definition:
* **x(Independent Variable):** ‘amount’, ‘oldbalanceOrg’, ‘newbalanceOrig’, ‘oldbalanceDest’, ‘newbalanceDest’, ‘type’
* **y(Dependent Variable):** ‘isFRaud’

### Data Spliting:
* Data splited using train_test_split into training and testing set
* Training set - **80%**, Testing set – **20%** 

---

## Model Evaluation And Comparison:

### Model Used:

* Logistic Regression(LR)
* Support Vector Machine(SVM)
* Random Forest(RF)
* Decision Tree(DT)

### Model Comparison:
<img width="1016" height="320" alt="image" src="https://github.com/user-attachments/assets/7e5b2790-f463-4e90-aa4a-02ecc3035ebf" />

<img width="579" height="326" alt="image" src="https://github.com/user-attachments/assets/a3a66437-a871-482c-88f9-fa5b325c7aba" />

### Inference:
* In our case precision is important as we don’t want to loose any customer by mis-predicting their transaction as fraud
* As per the requirement, Random Forest(RF) seems to be perfect model for fraud prediction

---

## Conclusion:

### Financial Impact:

* Net expected loss due to model’s error is 9 to 10 Million bucks
* Expected amount saved due to model’s correct prediction is 1.3 Billion bucks

### Limitation:

* The study relies on single dataset, potentially limiting its generalizability to diverse population
* The analysis only focus on time, balance, amount and type of transaction, overlooking on features such as IP address, customer history etc
* There is a lack of test dataset evaluation for model, which is a rising concern about its real world applicability

### Future Research:

Future research must ensure robustness, generalizability, and interpretability for informed decision-making based on study findings. It's important to check how duplicate data and unusual values affect the model's * accuracy. Creating strategies to deal with these issues is valuable for improving model performance.
