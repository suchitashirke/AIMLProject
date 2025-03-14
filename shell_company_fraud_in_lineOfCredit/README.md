### Project Title
**Fraud Detection for Shell Companies in Line of Credit Applications**

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

#### Research Question
***How can we create a predictive model to identify and prevent shell company fraud in SMB line-of-credit applications, reducing credit losses and mitigating fraud-related risks***

#### Data Sources
Data sources: https://www.kaggle.com/code/kevinm6720/sba-loan-approval-analysis#Data-Exploration Links to an external site., some of the data need to synthetically generate as well as pulled from my organizations test environment.

#### Methodology
1.	***Unsupervised Learning techniques*** like **Clustering** can be used for identifying patterns and anomalies and uncover potential fraudulent behavior in data related to shell company fraud. We can group similar applications or companies together in a cluster using **K-mean** to segment companies on characteristics such as revenue, credit amount requested, or age. Outliers can be flagged for further investigation. We can also create cluster for legitimate businesses while flagging shell companies as outliers.
2.	We can use ***PCA technique for dimensionality reduction*** considering various data aspect we have identified. This makes it easier to visualize patterns, identify clusters of potential shell companies, and enhance the performance of subsequent predictive models. PCA acts as a preprocessing step that can significantly improve the detection of fraudulent activities in credit applications. We can use PCA results as input feature for predictive models below.
3.	We can use ***Classification model like Logistic Regression, Decision Tree, SVM, K-Nearest Neighbor***. 

#### Results
For the Base Model has been document below

#### Next steps
For base Model next steps has been document below

#### Outline of project
Outline 1
Outline 2
Outline 3

#### Overview
Our company provides credit programs aimed at assisting small and medium-sized businesses (SMBs) in managing their cash flow through lines of credit. This service enables businesses to pay their bills even when immediate funds are unavailable, offering them flexibility and convenience.
Typically, businesses are assessed based on their financial health, cash flow, and payment history to determine eligibility and credit limits. Once approved, they can use this credit to pay vendors directly through our platform, with repayment terms that are usually flexible. Through our line of credit offerings, we help SMBs streamline their financial operations.
However, lines of credit can be vulnerable to various types of fraud, particularly "Shell Company Fraud." This fraudulent scheme involves creating fictitious businesses or utilizing real businesses with minimal operations to secure credit or loans without any intention of repayment. We aim to implement a scoring mechanism to detect potential shell company fraud in these applications.

### Data Set details: 
https://www.kaggle.com/code/kevinm6720/sba-loan-approval-analysis#Data-Exploration Links to an external site. And generated some of the columns utilizing the existing from the table. We have renamed some of the columns for better readability.

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


### The dataset collected is related to 17 campaigns that occurred between May 2008 and November 2010, corresponding to a total of 79354 contacts.

### Data Preprocessor and visualization:
1.	Load the dataset from the file 
2.	Check for the schema – column datatype and shape (columns and rows)
3.	Check for NaN values in the dataset. Used bar graph to see which has highest NULL values.
4.	Identify duplicates rows in the dataset and remove those duplicated rows. 
5.	Create a new column (Fraud/Shell company Fraud) which has categorical (PIF and CHGOFF), Changed those value to for binary data PIF= 0, CHGOFF=1.  Add it to data frame
6.	Used numeric features to identify the ***correlation matrix***
7.	Identified ***unique values*** for the categorical data
8.	Dropped columns – ***LoanNr_ChkDgt','ChgOffDate','ApprovalDate','ApprovalFY','DisbursementDate', 'Fraud Trend Over Time, Name, City, Bank, BalanceGross, ChgOffPrinGr, GrAppv, Sector_code, Frequence_of_apps due to same value for all record, post application values, duplicate column***
        ![image](https://github.com/user-attachments/assets/fb418917-6e55-4307-91a6-00f1d87f1fd8)
9.	**Plot graphs for univariant and bivariant**
      a.	Histogram (understand Distributions)– Annual Revenue, Term, DisbursementGross(Credit Requested)
  	      ![image](https://github.com/user-attachments/assets/335b758a-106b-4b09-a818-3da089f6751c)

      b.	BoxPlot (Identify the outliers) – Credit Score, NoEmp, DisbursmentGross (Credit Requested), NumofApplications, Annual Revenue, Net Income, CreateJob, RetainedJob
  	      ![image](https://github.com/user-attachments/assets/f4838bfe-c658-46d2-bbdd-841dc1017dff)

      c.	Barplot (to understand Frequency) – Payment Consistency, Purpose of credit, NAICS, State
  	      ![image](https://github.com/user-attachments/assets/0fac2d64-9a27-4807-aed7-71c622999251)

      d.	Pie Chart (To understand distribution) – RevLineCr, loan_backed_by_realEstate
  	      ![image](https://github.com/user-attachments/assets/c78873d1-a50c-418b-8d3f-ea6c2515754b)

      e.	Scatter plot (To understand distribution and relationship with target variable) – DisbursementGross (Credit Request) vs Annual Revenue, DisbursementGross (Credit Requested) vs NAICS, DisbursementGross (Credit Request) vs NoEmp,                DisbursementGross (Credit Request) vs Term along with Shell Company fraud
  	      ![image](https://github.com/user-attachments/assets/5480acac-8cd7-4577-9f52-b99040f09a9e)

      f.	Correlation heatmap
         ![image](https://github.com/user-attachments/assets/c7edd6cf-27a7-4a95-95dc-e7021c910b47)

### Engineering Features

1. **Imputed** Missing **Annual Revenue, outstanding loans with Median Value**. Also imputed values for missing **Fraud/Shell company Fraud, BankState, RevLineCr, payment_consistency, NewExist, State** by using **Mode** ( Most frequent Values)
2.	Applied **Binary Encoding to – FranchiseCode, loan_backed_realestate, lowDoc, Late Payment**
3.	Applied **Frequency Encoding for Zipcode RevlineCr**
4.	Applied **Ordinal Encoding for payment_consistency, Credit Utilizations, Tax_filed, Business License Status**
5.	Applied **Target Encoding for State and BankState**
6.	Applied **One Hot Encoding for NAICS and Purpose_of_credit**
7.	Removed **Outliers** to reduce the noise using **IQR and log transformation** technique. This helped reduce the data size and removed outliers
   	Credit Score, NoEmp, NumOfapplications, Annual_Revenue, Net_Income, Term
8. Log transformation to **disbursementGross**

### Unsupervised Model****
Applied Unsupervised Learning like Clustering using K-Means.
   ![image](https://github.com/user-attachments/assets/9d3bd776-debc-4755-ac48-c29ee4fca88e)
   ![image](https://github.com/user-attachments/assets/02a2ea59-c364-4fb4-ad6b-8304eabebf50)
   
   a.	Fraud Distribution by Cluster: Cluster 0 - 8594.0 , Cluster 1 - 1871.0, Cluster - 2 - 303.0,  Cluster 3-  2397.0
   b.	Financial and loan characteristics by cluster
   ![image](https://github.com/user-attachments/assets/acdc7c77-3390-4409-ab7d-3d5de78f07a5)

### Train/Test Split: 
Split the data into Train and test by using 80/20 combination. 80% - train data and 20% - test data and dropping the target variable from the data frame. We use all the columns int/float except the dropped ones

### Model Metrics
Ran Baseline model – DummyClassifier, SVC( baseline) 
Ran Models like LogisticRegression, DecisionTreeClassifier, KNN, SVM 

![image](https://github.com/user-attachments/assets/d93c863c-f1f8-4510-8d8b-14bb4eaf6715)

![image](https://github.com/user-attachments/assets/35d168b8-221b-4a51-a45b-b010910ff7b0)

#### Key Observations
1. Decision Tree has the highest accuracy (87.8%) and F1-score (70.8%) on test data, but it may overfit (100% accuracy on training).
2. Logistic Regression is well-balanced (79.7% accuracy, 51.6% precision, 30.1% F1-score).
3. SVM (default settings) is failing (0 Precision, 0 Recall, 0 F1-score), likely due to class imbalance or poor hyperparameter choice.

### Next Step:
1.	We might want to use Feature engineering to improve the data quality
a.	Using Recursive Feature Elimination (RFE)
b.	Feature Scaling 
2.	Address the class imbalance especially for SVM models
3.	Using Ensemble like Boosting for model selection and stacking
4.	More hyperparameter tuning
