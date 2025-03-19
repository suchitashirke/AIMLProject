### Fraud Detection for Shell Companies in Line of Credit Applications

#### Executive summary

**Project overview and goals:**

Our company provides **credit programs** aimed at assisting small and medium-sized businesses (SMBs) in managing their cash flow through lines of credit. This service enables businesses to pay their bills even when immediate funds are unavailable, offering them flexibility and convenience.
Typically, businesses are assessed based on their **financial health, cash flow, and payment history** to determine eligibility and credit limits. Once approved, they can use this credit to pay vendors directly through our platform, with repayment terms that are usually flexible. Through our line of credit offerings, we help SMBs streamline their financial operations.
However, **lines of credit can be vulnerable** to various types of **fraud**, particularly **"Shell Company Fraud."** This fraudulent scheme involves creating **fictitious businesses or utilizing real businesses with minimal operations** to secure credit or loans without any intention of repayment. We aim to implement a scoring mechanism to detect potential shell company fraud in these applications.

### Rationale

***Brand Impact:***
If we fail to address shell company fraud, it could lead to significant financial losses, 
damaged relationships with legitimate SMB clients, and reputational harm. 
Fraudulent entities not only drain resources but also erode the trust that legitimate businesses place in our credit services.

***Business Impact:***
This analysis provides actionable intelligence to strengthen fraud prevention mechanisms. By accurately identifying potential shell companies, 
we can:
1. Protect the company’s financial health by minimizing defaulted loans.
2. Enhance customer trust and retention by focusing resources on serving legitimate SMBs.
3. Optimize manual review efforts by automating initial risk assessments, saving time and reducing operational costs.
   
***Overall Importance:***
Shell company fraud undermines the integrity of financial systems. 
Detecting and preventing it contributes to a fairer and more sustainable credit market for SMBs, allowing genuine businesses to thrive. 
This aligns with our mission to empower SMBs while safeguarding the company and the broader economy from fraudulent activities.

### Research Question

***How can we create a predictive model to identify and prevent shell company fraud in SMB line-of-credit applications, reducing credit losses and mitigating fraud-related risks***

### High Level Methodology

1.	***Unsupervised Learning techniques*** like **Clustering** can be used for identifying patterns and anomalies and uncover potential fraudulent behavior in data related to shell company fraud. We can group similar applications or companies together in a cluster using **K-mean** to segment companies on characteristics such as revenue, credit amount requested, or age. Outliers can be flagged for further investigation. We can also create cluster for legitimate businesses while flagging shell companies as outliers.
2.	We can use ***PCA technique for dimensionality reduction*** considering various data aspect we have identified. This makes it easier to visualize patterns, identify clusters of potential shell companies, and enhance the performance of subsequent predictive models. PCA acts as a preprocessing step that can significantly improve the detection of fraudulent activities in credit applications. We can use PCA results as input feature for predictive models below.
3.	We can use ***Classification model like Logistic Regression, Decision Tree, SVM, K-Nearest Neighbor***. 

### Data Set details: 

https://www.kaggle.com/code/kevinm6720/sba-loan-approval-analysis#Data-Exploration Links to an external site. And generated some of the columns utilizing the existing from the table. We have renamed some of the columns for **better readability**. Like **MIS_Status was changed to  Fraud/Shell company Fraud** . **DisbursementGross (referred as Credit Requested)**. I have also use synthetic way to generate certain other columns which are normally used for decisioning in Credit line business. The notebook for generating these synthetic columns is also added.  **Ideal way is to integrate with vendors like Experian/TransUnion as well as LexisNexis who can provide this information.**

### Input variables:

***Compay Information:***
-	LoanNr_ChkDgt: Identifier – Primary key
-	Name: Borrower name
-	City: Borrower City
-	State: Borrower State
-	Zip: Borrower zip code - INT
-	Bank: Bank name
-	BankState: Bank state
-	NAICS (Categorial): North American industry classification system code 
-	ApprovalDate: Date SBA commitment issued - INT
-	ApprovalFY: Fiscal year of commitment - INT
-	Term: Loan term in months - INT
-	NoEmp: Number of business employees - INT
-	New Exist: 1 = Existing business, 2 = New business - INT
-	CreateJob: Number of jobs created - INT
-	RetainedJob: Number of jobs retained - INT
-	FranchiseCode: Franchise code, (00000 or 00001) = No franchise- INT
-	UrbanRural (Categorial): 1 = Urban, 2 = rural, 0 = undefined -
-	Sector_Code:  Description of the first two digits of NAICS - INT

***Application Characteristics:***
-	DisbursementDate: Disbursement date - OBJECT
-	DisbursementGross: Amount disbursed/Requested - FLOAT
-	BalanceGross: Gross amount outstanding - FLOAT
-	RevLineCr (Categorial): Revolving line of credit: Y D Yes, N D No
-	LowDoc (Categorial): LowDoc Loan Program: Y D Yes, N D No
-	loan_backed_realestate (Categorial): = 1 if loan is BACKED by real estate, = 0 NOT BACKED
-	purpose of credit (Categorial): Usage of Credit Amount
-	RevLineCr (Categorial): Revolving line of credit: Y = Yes, N = No

***Financial Data:*** 
-	Annual Revenue: Annual Revenue of Borrower- FLOAT
-	Net Income: Net Income of Borrower - FLOAT

***Behavior data:***
-	NumOfapplications – Num of credit applications - INT
-	Frequence_of_apps (Categorial)– Frequency of applications -HIGH, LOW
-	payment_consistency (Categorial) – Repayments – Regular, Periodic, Sporadic, NONE

***External Data Source:***
-	Credit Utilizations (Categorial): Credit Utilizations done by Borrower- HIGH, LOW, NO DATA 
-	Late Payments (Categorial): Late Payments by Borrower – YES or NO
-	Taxed_filed (Categorial): Taxed Filed for the Company by Borrower - YES, NO, PENDING, LATE, EXEMPT
-	Business license State (Categorial): Business license Status - EXPIRED, RENEWAL DUE, UNDER AUDIT, NOT REQUIRED, YES, NO
-	Outstanding loans: Number of Outstanding loans INT

***Historical data:***
-	Fraud Trend Over time for industry (Categorial) – STABLE, UNSTABLE
-	Fraud incident (Categorial) – YES or NO

***Output variable (desired target):***
1.	Fraud/Shell company Fraud (Categorial) – ***PIF (PAID IN FULL) or CHGOFF (CHARGED OFF)***

### Data Preprocessor and visualization:

1.	Load the dataset from the file diretory **"data/latest_shell_company_fraud_dataset.csv"**
2.	Check for the schema – column datatype and shape (columns and rows)
3.	Check for NaN values in the dataset. Used bar graph to see which has highest NULL values.
4.	Identify duplicates rows in the dataset and remove those duplicated rows. 
5.	Create a new column (Fraud/Shell company Fraud) which has categorical (PIF and CHGOFF), Changed those value to for binary data PIF= 0, CHGOFF=1.  Add it to data frame
6.	Used numeric features to identify the ***correlation matrix***
7.	Identified ***unique values*** for the categorical data
8.	Dropped columns – ***LoanNr_ChkDgt','ChgOffDate','ApprovalDate','ApprovalFY','DisbursementDate', 'Fraud Trend Over Time, Name, City, Bank, BalanceGross, ChgOffPrinGr, GrAppv, Sector_code, Frequence_of_apps due to same value for all record, post application values, duplicate column***
   
       ![image](https://github.com/user-attachments/assets/b4559e65-4883-4c87-b2ba-ce80214e0508)
       **Interpretation:**
  	      This graph indicated which fields has most missing value. ChgOffDate has most missing percentage about ~89%.
  	
9. **Plot graphs for univariant and bivariant**
    
      a.	**Histogram** (understand Distributions)– Annual Revenue, Term, DisbursementGross(Credit Requested)
         ![image](https://github.com/user-attachments/assets/5eca6e3c-c539-4d55-a54f-4360d438590c)
         ***Interpretation**
   
         1.	Annual Revenue - Highly right-skewed distribution → Most businesses have low revenue, with a few having very high revenue.  Large values could be outliers or belong to a small number of high-revenue firms.
         2.	Loan Term: The distribution has multiple peaks, indicating common loan durations (e.g., 100, 200, 300 months). Suggests loan term policies might be standardized into specific ranges.
         3.	Credit Request: Also, right-skewed, indicating most credit requests are small, with a few extremely large requests. Suggests a small number of businesses request very high loans.
         We can remove the extremely high value outlier ones using Zscore. Use log transformation to normalize the values

      b.	**BoxPlot** (Identify the outliers) – Credit Score, NoEmp, DisbursmentGross (Credit Requested), NumofApplications, Annual Revenue, Net Income, CreateJob, RetainedJob
     	      ![image](https://github.com/user-attachments/assets/b63d6c82-53a7-46a7-a369-2bf5a4a42ee5)
         **Interpretation:**
   
         1.	Credit Score & NoEmp → Distribution is normal, but some outliers exist. 
         2.	DisbursementGross, Annual Revenue, Net Income → Show significant outliers, indicating potential data errors or genuine business anomalies. 
         3.	Number of Applications, CreateJob, RetainedJob → Also have extreme values, which might indicate policy-related constraints or errors.
         We can use **IQR or log transformation to remove outlier**

      c.	**Barplot** (to understand Frequency) – Payment Consistency, Purpose of credit, NAICS, State
         ![image](https://github.com/user-attachments/assets/579507c2-8aaa-4042-bf23-25807d9cfe61)
         **Interpretation:**
   
          1.	Payment Consistency:
               a.	Most businesses have "Regular" payment consistency, while only a small portion are "Sporadic" or "Periodic".
               b.	The imbalanced distribution suggests that delayed payments might be rare, or reporting may be biased.
          2.	Purpose of Credit:
               a.	Distribution is evenly spread, suggesting different businesses apply for credit for various purposes.
               b.	However, some categories might be more critical for risk assessment.
          3.	NAICS (Industry) Classification:
               a.	Manufacturing, Retail, and Construction dominate the dataset.
               b.	Less representation from Utilities, Public Administration, and Military suggests that certain industries may have lower credit needs.
          4.	State-wise Distribution:
               a.	California has the highest count → This could indicate a high number of businesses applying for credit in CA.
   	         b. Some states have very low representation, which may affect generalization for models

         Using Target/Frequency or one hot encoding for improved model performance
   	
      d.	**Pie Chart** (To understand distribution) – RevLineCr, loan_backed_by_realEstate
            ![image](https://github.com/user-attachments/assets/fd6f7792-bfe8-4b87-acf2-bbe5b44b4515)
         **Interpretation:**
   
   	   1.	Revolving Line of Credit indicated – 49.8% do not have revolving credit vs 27.2 show revolving credit as yes. Rest 27.5 are showing as 0
         2. 76.4 % are not backed with real Estate whereas 23.6 are backed.  There is possibility that 23.6 % might have higher risk profile leading to different load approval criteria.

      e.	**Scatter plot** (To understand distribution and relationship with target variable) – DisbursementGross (Credit Request) vs Annual Revenue, DisbursementGross (Credit Requested) vs NAICS, DisbursementGross (Credit Request) vs NoEmp,                DisbursementGross (Credit Request) vs Term along with Shell Company fraud
            ![image](https://github.com/user-attachments/assets/c75b9309-a5a8-47fe-9a15-f3bd93a42bfd)
         **Interpretation:**

         1.	Clear positive correlation between DisbursementGross( Credit Requested vs Annual Revenue. A few fraudulent cases (orange dots) appear at different revenue levels, indicating that fraud is not restricted to low-income businesses.
         2.	 Different industries show varying levels of credit requests, but fraud cases (orange dots) are scattered across industries.  Manufacturing, Construction, and Retail Trade dominate loan requests, suggesting industry-specific                   lending patterns.
         3.	Most businesses have fewer employees (below 2000), even for high loan requests. Fraudulent cases appear mostly in lower employee count businesses, suggesting that fraud is more common in smaller companies
         4.	Loan terms range widely, but fraud cases exist across all loan term ranges. No clear trend linking fraud to shorter or longer loan terms, so other factors (like revenue or industry) may be more critical

      f.	**Correlation heatmap**
         ![image](https://github.com/user-attachments/assets/0219d194-b7a3-4f9e-ba25-e15e3f85cf87)
         **Interpretation:**

         1.	Strong correlation between Annual Revenue & Net Income (0.93) → Higher revenue is naturally associated with higher profit. 
         2.	High correlation between DisbursementGross & Annual Revenue (0.92) → Businesses with higher revenue tend to request larger loans. 
         3.	Fraud/Shell Company Fraud negatively correlates with Term (-0.30) & NumOfApplications (-0.27) → Fraudulent businesses may prefer shorter loan terms and fewer applications. 
         4.	Weak correlation between Credit Score & Fraud (-0.47) → Lower credit scores might be weakly indicative of fraud.

         Features highly correlated with each other might not add extra value in modeling.

### Engineering Features

1. **Imputed** Missing **Annual Revenue, outstanding loans with Median Value**. Also imputed values for missing **Fraud/Shell company Fraud, BankState, RevLineCr, payment_consistency, NewExist, State** by using **Mode** ( Most frequent Values)
2.	Applied **Binary Encoding to – FranchiseCode, loan_backed_realestate, lowDoc, Late Payment**
3.	Applied **Frequency Encoding for Zipcode RevlineCr**
4.	Applied **Ordinal Encoding for payment_consistency, Credit Utilizations, Tax_filed, Business License Status**
5.	Applied **Target Encoding for State and BankState**
6.	Applied **One Hot Encoding for NAICS and Purpose_of_credit**
7.	Removed **Outliers** to reduce the noise using **IQR and log transformation** technique. This helped reduce the data size and removed outliers
   	**Credit Score, NoEmp, NumOfapplications, Annual_Revenue, Net_Income, Term**
8. Log transformation to **disbursementGross**

### Unsupervised Model
Applied Unsupervised Learning like Clustering using K-Means with **optimal K = 4** based on the Elbow Method
   a.	Fraud Distribution by Cluster: Cluster 0 - 8594.0 , Cluster 1 - 1871.0, Cluster - 2 - 303.0,  Cluster 3-  2397.0
   b.	Financial and loan characteristics by cluster
   ![image](https://github.com/user-attachments/assets/28201313-80d3-4f6f-ad44-2627131f10b1)
   ![image](https://github.com/user-attachments/assets/4021ac02-c2fc-424c-aadf-f7af6a67a8ce)
   ![image](https://github.com/user-attachments/assets/c7533ab7-f2d7-43a4-9bdd-f634602a3622)


### Train/Test Split: 
Split the data into Train and test by using 80/20 combination. 80% - train data and 20% - test data and dropping the target variable from the data frame. We use all the columns int/float except the dropped ones

### Base Model Metrics

Ran Baseline model – DummyClassifier, SVC( baseline) 
Ran Models like LogisticRegression, DecisionTreeClassifier, KNN, SVM

![image](https://github.com/user-attachments/assets/73794108-e652-4050-b99c-32c3c42e8c98)

**Key Observations for Base Model Metrics**
   1.	Decision Tree has the highest accuracy (87.8%) and F1-score (70.8%) on test data, but it may overfit (100% accuracy on training).
   2.	Logistic Regression is well-balanced (79.7% accuracy, 51.6% precision, 30.1% F1-score).
   3. SVM model performs well on training data but fails on the test set, as seen by the drastic drops in recall (0.24) and F1-score (0.33). High Precision(0.53), Low Recall(0.24): The test precision is relatively higher than recall, meaning       the model is making very few false positive predictions but missing many actual positive cases. SVM is worst model as it required a lot of execution time.
   4. KNN model performs better on the training set compared to the test set, indicating overfitting. Low Recall(0.27) The model struggles to capture positive cases in the test set, meaning it may not be ideal for high-risk applications.
      KNN provides decent accuracy(0.78) but lacks strong precision and recall in the test set.
      
   ![image](https://github.com/user-attachments/assets/651a3b9e-9dfa-49b5-96cf-e20273232992)

### Tuned Model Metrics with ensemble technique 
   ![image](https://github.com/user-attachments/assets/be4037c8-cd7c-428b-8c00-2335217eb2ee)

### Key Observations
   1.	**XGBoost** is the best performing model with accuracy around **92.37%, low precision 90.9% ( Low false positive), Recall around 84.39%** Strong ability to detect true positives. And **F1-score of 81.99%** best balance between recall 
      and precision. Considering the imbalance of class XGBoost is performs best. We should focus on using XGBoost as our primary model for making decision whether to approve the line of credit loan for small businesses. XGBoost also               performed well in consideration of **execution time – 78 seconds**
   2.	**Random Forest (Tuned), Boosted RF, and Stacking RF show 100% train accuracy**, but **lower test accuracy, suggesting overfitting.** Training accuracy shows that model memorize training data but don’t generalize the unseen data as in        both cases the test accuracy is less than 90%. If this model used, it might give us certain overconfidence that may lead to risky decision like approving fraudulent loans by shell companies.
   3.	**SVM (Tuned) has the lowest accuracy (77.05%)**, making it the weakest performer.
   4.	**Logistics Regression** - Logistic Regression has the **lowest recall (0.21)**, indicating it misses many fraudulent cases. 
   5.	Both **SVM and logistics Regression** has **lower F1-score** making them less effective. 
   6.	Considering the execution **SVM is slowest of all 589 seconds**, making it impractical for real time line of credit application evaluation.

**Plot for Overall Model(Tuned) Metrics***
![image](https://github.com/user-attachments/assets/39df5684-82f7-46ed-9e27-9dfd20c2d75c)

**Plots for feature importance in logistic Regression and XGBoost**
![image](https://github.com/user-attachments/assets/ec450136-1666-400c-ae5d-cc596316a421)
![image](https://github.com/user-attachments/assets/6ec677ff-5d98-4be5-86f1-b7d7e3880a5a)

### Findings:

The best model for detecting fraud in loan applications is the **XGBoost Classifier**, with an **accuracy of 0.9237, recall of 0.8439, and F1-score of 0.81992**. It balances precision and recall effectively, making it the most reliable.
**Random Forest (Tuned) and Boosted Random Forest** show perfect training performance but **overfit, leading to lower generalization**. **Logistic Regression and KNN** struggle with recall, making them **less effective in detecting fraud**.
**XGBoost is the best choice**, offering strong performance without overfitting. Further improvements can be made by adjusting classification thresholds based on business risk to enhance fraud detection. As well as using ensemble technique like stacking can be used to improve the metrics. 

### Results and conclusion:

The **XGBoost Classifier** emerged as the best-performing model for fraud detection, achieving an accuracy of 0.9237, recall of 0.8439, and F1-score of 0.81992. It provides a strong balance between precision and recall, making it suitable for identifying fraudulent loan applications by Shell Companies.Random Forest (Tuned) and Boosted Random Forest showed perfect training accuracy, indicating overfitting, which reduces their generalization to new data. Logistic Regression and KNN models had lower recall, making them less effective in detecting fraud cases. Overall, **XGBoost is the most reliable model** and should be deployed with further optimizations, such as dynamic classification thresholds based on business risk and feature selection improvements to enhance fraud detection while minimizing false positives.

### Future Research and Development for fraud detection during line of credit applications

1.	XGBoost performance is best but its still a black box model which lacks transparency in how the decisions are been taken. Using Explainable Boosting Machine EBM will help us understand fraud trends better which help explain the prediction more succinctly unlike XGBoost. 
2.	Exploration of EBM will enable us to detect bias and fairness adjustment. The predictive power for EBM might be lower than XGBoost. 
Now based on business needs if transparency and fairness are critical and eliminating biases is important than we should go with EBM over XGBoost. EBM will give us those insight which we can use in preprocessing steps to have more concreate data sampling.
3.	Fraud Patterns evolves requiring adaptive decision making and reinforcement learning. We can take predictive decision of XGBoost model and use it for risk scoring based on certain thresholds or using logarithmic or percentile-based scaling.

### Next steps and recommendations:

1.	**Deploy** the XGBoost model in (test/Sandbox) environment and test the performance of the model before we deploy it in production
2.	**Monitor the false positive and false negative rate** to fine-tuned decision thresholds
3.	Current model is completely based on Company, financial attributed. Such attributes can be manipulated. Hence, we can **enhance** model prediction by using **device fingerprinting** (device from the loan are been applied), **document verification status** as well as **IP tracking**, utilize **linkages to other fraud applications** by using network graphs between application attribute – same device ID, IP, Proximity of device from where loans are applied vs the actual address on the application.  
4.	Set up **automated model retraining** to adapt to fraud trends.

Additionally, further work can be done in **improving the performance of XGBoost by improving the data quality and feature engineering, balancing the classes using SMOTE, weight balancing, using stacking ensemble (XGBoost + RandomForrest) or (XGboost + Logistic Regression)**

### Contact Information

Suchita Shirke

[[LinkedIn](linkedin.com/in/suchitashirke)]


