## Overview:
In this practical application, your goal is to compare the performance of the classifiers we encountered in this section, namely K Nearest Neighbor, Logistic Regression, Decision Trees, and Support Vector Machines. We will utilize a dataset related to marketing bank products over the telephone.

### Business Objective of the Task
The goal is to develop a data-driven predictive model that can identify clients/customers most likely to subscribe to the bank’s long-term deposit product, based on demographic, behavioral, and economic context attributes. By doing so, the bank aims to achieve the following objectives:
- Improve campaign effectiveness by increasing the subscription success rate while reducing unnecessary customer contacts.
- Reduce operational overhead by focusing resources on high-probability clients.
- Optimize marketing strategies by leveraging insights from data to design campaigns for maximum conversions.
- Increase revenue growth through higher adoption of the long-term deposit product.

### Data Used:
Our dataset comes from the UCI Machine Learning repository link. The data is from a Portugese banking institution and is a collection of the results of multiple marketing campaigns. We will make use of the article accompanying the dataset here for more information on the data and features.
Understanding the Data: How many marketing campaigns does this data represent?

### Input variables:

**Bank client data:** 
1.	Age : Age of the lead (numeric)
2.	Job : type of job (Categorical)
3.	Marital : Marital status (Categorical)
4.	Education : Educational Qualification of the lead (Categorical)
5.	Default: Does the lead has any default(unpaid)credit (Categorical)
6.	Housing: Does the lead has any housing loan? (Categorical)
7.	loan: Does the lead has any personal loan? (Categorical)

**Related with the last contact of the current campaign:**
1.	Contact: Contact communication type (Categorical)
2.	Month: last contact month of year (Categorical)
3.	day_of_week: last contact day of the week (categorical)
4.	duration: last contact duration, in seconds (numeric).

**Other attributes:**
1.	campaign: number of contacts performed during this campaign and for this client (numeric)
2.	pdays: number of days that passed by after the client was last contacted from a previous campaign(numeric; 999 means client was not previously contacted))
3.	previous: number of contacts performed before this campaign and for this client (numeric)
4.	poutcome: outcome of the previous marketing campaign (categorical)

**Social and economic context attributes**
1.	emp.var.rate: employment variation rate - quarterly indicator (numeric)
2.	cons.price.idx: consumer price index - monthly indicator (numeric)
3.	cons.conf.idx: consumer confidence index - monthly indicator (numeric)
4.	euribor3m: euribor 3 month rate - daily indicator (numeric)
5.	nr.employed: number of employees - quarterly indicator (numeric)

### Output variable (desired target):

1.	y - has the client subscribed a term deposit? (binary: 'yes','no')

### The dataset collected is related to 17 campaigns that occurred between May 2008 and November 2010, corresponding to a total of 79354 contacts.

### Data Preprocessor and visualization:
1.	Load the dataset from the file 
2.	Check for the schema – column datatype and shape (columns and rows)
3.	Check for NaN values in the dataset. This dataset has no null values
4.	Identify duplicates rows in the dataset and remove those duplicated rows. DataSet had 12 duplicate rows
5.	Create a new column (y_numeric) which has numerical values for binary data Yes= 1, No=0. Add it to data frame
6.	Change categorical data housing, default, loan to Yes=1, No=0, unknown = -1
7.	Drop columns cons.price.idx, cons.conf.idx after checking the correlation
8.	Plot graphs for univariant and bivariant
   
    a.	Bar plot – Success rate by job, education , marital status
    b.	Boxplot – Age vs Target, duration vs Target
    c.	Histogram – campaign calls distributions
    d.	Hist – Previous contact distributions
         ![image](https://github.com/user-attachments/assets/dca01c0d-9ad9-4b56-a4a3-9be64df0e774)

  	g.	Correlation heatmap
        ![image](https://github.com/user-attachments/assets/27795839-92f2-438d-87bd-d57fd238f610)
  	    ***Insights from HeatMap***
  	    1. The indicators have correlation among themselves.
  	  	2. Number of employees rate is highly correlated with employee variation rate.
  	  	3. Consumer price index is highly correlated with bank interest rate( higher the price index, higher the interest rate).
  	  	4. Employee variation rate also correlates with the bank interest rates

  	e.	Boxplot – duration vs job
  	f.	Scatterplot – duration vs campaign
        ![image](https://github.com/user-attachments/assets/36b5b8ad-55e7-47bd-8c67-b2c14277ebcd)
  	    ***Insights from duration vs job:***
  	    1. The leads who have not made a deposit have lesser duration on calls.
  	    2. Comparing the average, the blue collar, entrepreneur have high duration in calls and student, retired have less duration in average.
  	    3.  Large distribution of leads were from self employed clients and management people.
  	
  	   ***Insights from duration vs campaign:***
  	    1. The more the duration the calls were, they had higher probability in making a deposit
        2. Duration of calls faded as the time period of campaign extended further
        3. There were many positive leads in the initial days of campaign
10. Based on the correlation heatmap, we can remove/drop the columns like default, housing, loan as they 

### Engineering Features

1.	Apply ***OneHotEncoding***  to certain columns - 'job', 'marital', 'education', 'poutcome’, ‘contact’
2.	***Remove outliers*** from age, campaign, duration column using IQR as some model like SVM are sensitive to outliers 
3.	Convert the ***month and days_of_week*** column to integer using maps
4.	***Pdays*** has many 999 values, we mapped those 0

### Train/Test Split: 
Split the data into Train and test by using 70/30 combination. 70% - train data and 30% - test data and dropping the target variable from the data frame. We use all the columns int/float except the dropped ones

### Model Metrics:

#### Model accuracy for logistics Regression with ensemble is – 94%

![image](https://github.com/user-attachments/assets/d44782c6-fedd-4caa-9fe2-7bd2d630c298)

#### Summary of Classification Model Performance

![image](https://github.com/user-attachments/assets/2a861fe8-ad71-439e-892a-e6f479d9a3cf)

![image](https://github.com/user-attachments/assets/0aaf01f2-b5fe-48a6-9134-7a71350fd054)

![image](https://github.com/user-attachments/assets/a46aa1f5-0db5-4ad8-a850-2f8d89879150)

#### Key Observations
1. **Baseline Performance:**
   - The Dummy Classifier serves as a baseline with very low scores across all metrics, highlighting the benefit of using predictive models.
2. **Logistic Regression:**
   - Logistic Regression (Tuned) is one of the best models for this task, demonstrating consistently high accuracy, precision, and F1 scores on both training and testing sets.
   - Performs well without significant overfitting.
   - Offers strong interpretability.
   - Maintains a good balance between training and test scores.
3. **Tree-Based Models (Random Forest & Decision Tree):**
   - **Random Forest (Tuned):** Shows strong metrics, particularly high precision and F1 score on the test set, indicating robustness and high-quality predictions. Suitable for precision-focused tasks.
   - **Decision Trees (Default):** Underperform compared to the tuned Random Forest, suggesting that tuning and ensemble techniques are crucial for tree-based models. A significant gap between training and testing scores indicates overfitting.
4. **SVM Models:**
   - The tuned SVM shows excellent recall for both training and testing datasets, making it suitable for tasks where identifying all positive cases is a priority.
   - Slight overfitting is evident, as training scores are higher than testing scores.
   - The default SVM required tuning for better performance. While accuracy and recall are good, low precision indicates a high rate of false positives (e.g., customers identified as likely to subscribe but did not subscribe).
   - Computationally intensive and time-consuming.
5. **K-Nearest Neighbors (KNN):**
   - Tuned KNN shows balanced performance but does not outperform Random Forest or SVM models, indicating limited suitability for this problem. It has higher precision but lower recall, indicating false negatives (e.g., customers identified as unlikely to subscribe but did subscribe).
   - KNN (Default) shows lower test accuracy and F1 scores compared to other models, suggesting inferior performance.
6. **Tuning Impact:**
   - Tuning significantly improves the metrics across all models (e.g., Logistic Regression, SVM, Random Forest), emphasizing the importance of hyperparameter optimization.
7. **Generalization:**
   - Models like Logistic Regression and Random Forest generalize well, with small differences between training and testing scores, indicating stability.


#### Model Performance Insights & Next Steps

##### 1. Precision vs. Recall Trade-Off
- **Random Forest:** Best for minimizing false positives, ideal when high precision is critical.
- **SVM (Tuned):** Best for maximizing the identification of positive cases, ideal when high recall is important.

##### 2. Balanced Models
- **Logistic Regression** provides a robust balance between precision and recall, making it a reliable model for deployment without overfitting.

##### 3. Specialized Use Cases
- **Precision-focused tasks**: Use **Random Forest**.
- **Recall-focused tasks**: Use **SVM** (tuned) for recall-critical tasks in specific marketing campaigns.

#### Next Steps
1. **Refine Model Performance:**
   - Continue hyperparameter tuning to improve model accuracy.
2. **Feature Engineering:**
   - Identify and integrate additional features to enhance the model's predictive power.
3. **Explore Model Ensembling:**
   - Investigate stacking techniques to combine the strengths of multiple models.
4. **Test Unseen Data:**
   - Validate the models using new data to assess generalization.
5. **Confusion Matrix Analysis:**
   - Use confusion matrix analysis to understand the impact of false positives and false negatives on business outcomes.
6. **A/B Testing:**
   - Conduct A/B testing on model predictions to evaluate performance in real-world scenarios.
7. **Feedback Loop:**
   - Gather continuous feedback from campaign results to retrain and improve the model over time.
  
   
#### Overall Recommendations
##### Best Overall Model:
- **Tuned Logistic Regression:** Provides the best balance between precision and recall, with a high F1 score ensuring optimal performance for both metrics. It is also interpretable, making it a strong choice for deployment.
##### Precision-Focused Model:
- **Random Forest (Tuned):** Focuses on targeting fewer, more likely customers. Ideal when minimizing false positives and maximizing precision is a priority.
##### Recall-Focused Model:
- **SVM (Tuned):** Ensures that the maximum number of potential customers are captured, even if it means some uninterested customers are included. Best when maximizing recall is crucial.

**Integration with Marketing Automation:**  
  The models, particularly the tuned Random Forest and SVM, should be integrated into the marketing automation system to perform real-time targeting of viable customers who are likely to subscribe.
  We should continuously monitor model performance after deployment and track metrics such as precision, recall, and F1 score to ensure models are meeting campaign objectives. 
  We should regularly update and adjust the models based on performance feedback and new data. Establish a continuous feedback loop to retrain the models using campaign results to refine predictions and improve customer targeting over time.

