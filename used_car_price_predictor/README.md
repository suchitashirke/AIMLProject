What Drives the Price of a Car?

As per our objective of identifying the key drivers that influence used car prices.
We need to understand how each of the factors will help provide insights for setting competitive prices and optimizing inventory management
We used 3 models here **1. Linear Regression 2. Ridge Regression 3. Lasso Regression** Below are the Metrics Evaluation for each of them:

**Linear Regression:**
RMSE: 96,617,279
R²: 0.462
MAE: 7,041
The above metrics shows that moderate prediction accuracy. The scatter plot indicates error in predictions of prices as the points are not closely aligned with the diagonal line of linear regression.

**Ridge Regression:**
RMSE: 96,253,632
R²: 0.463
MAE: 7,036
Similar to Linear Regression, even with regularization not significantly improving the model performance. However, the results are consistent for RMSE even with different alpha values. Seems regularization had not given any uplift in model performance. 
The residual histogram also confirms variability in predictions errors. Tails of graphs show higher prediction errors and maybe it is struggling with available data

**Lasso Regression:**
RMSE: 9,811 (Best performance)
R²: 0.463
MAE: 7,010
Lasso seems to offers the best prediction accuracy with lowest RMSE as compared to Linear and Ridge regression, but the model does not predict well considering the variance where around 46% of variance in car prices. 
Both graph (scatter and histogram) confirms that model performance is skewed for certain set of data.

**Business objective** was to understand the drivers of used car prices and build a model that can predict used car prices effectively.
Findings We used the above 3 models and based on the data **Lasso regression appears to be the most effective** in terms of predictive accuracy due to the significantly lower RMSE. 
However, the **R2 score** for each model suggests that model is not capturing most of the **variance** in the target variables, 
approximately **50%** of predicted values are either **underpredicted or overpredicted. Using regularization with hyperparameters also did not help in improving the performance of model.** 
This indicate that the model might not be providing meaningful insights or relevance about the factors that influences the used car prices. Keys insights based on the **model coefficients** are,

•**Car_age and odometer** have the largest impact on used car price. Car with higher mileage have lesser price due to wear and tear. Similarly older cars have less value compared to new ones.
•	Categorical feature like car **condition** suggests that car with good conditions is priced higher as compared with condition like new.
•	Car with **4-wheel drive** is priced higher than car with front wheel (FWD) and rear wheel drive (RWD).

Even though linear regression provides some insights on the car price, the predictive accuracy is not high enough to provide reliable pricing for unseen cars that gets added to inventory. 
Overall conclusion is all the 3 models do not give us required confidence that the factor chosen are deriving and predicting car prices. The results seem to be inconclusive.

**Recommendation** 
To be more conclusive on the drivers for the car price, we might want to used different models that could explain more variance. 
We need to revisit or add certain features in the models along with their correlation to draw better insights. 
Maybe adding other features or computing certain feature maybe led us to better model accuracy. 
Considering the R2 score, maybe using more complex models to capture more of the variance in price variable will be effective. 
Further hyperparameter tuning might help us overcome underfitting and overfitting of model.


**Notebook Link**: https://github.com/suchitashirke/AIMLProject/blob/main/used_car_price_predictor/used_car_price_predictor.ipynb 
