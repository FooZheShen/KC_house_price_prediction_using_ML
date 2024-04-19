# Predicting King County House Prices using ML

## Introduction
![image](https://github.com/FooZheShen/KC_house_price_prediction_using_ML/assets/153910230/d1d62863-2194-4c0f-af55-bd6990ad8c69)

For this project, I am tasked by the Real Estate Agency to identify key features of a home when trying to predict the house prices for future use 
when dealing with clients looking to sell or buy houses in King County.

I will be building a Multiple Regression Model to analyze and predict house sales in a northwestern county using the King County Sales dataset that has been provided.

This report discusses the steps, procedures, assumptions, and validation methods used for my analysis.



### Column Names and descriptions for Kings County Data Set
* **id** - unique identified for a house
* **dateDate** - house was sold
* **pricePrice** -  is prediction target
* **bedroomsNumber** -  of Bedrooms/House
* **bathroomsNumber** -  of bathrooms/bedrooms
* **sqft_livingsquare** -  footage of the home
* **sqft_lotsquare** -  footage of the lot
* **floorsTotal** -  floors (levels) in house
* **waterfront** - House which has a view to a waterfront
* **view** - Has been viewed
* **condition** - How good the condition is ( Overall )
* **grade** - overall grade given to the housing unit, based on King County grading system
* **sqft_above** - square footage of house apart from basement
* **sqft_basement** - square footage of the basement
* **yr_built** - Built Year
* **yr_renovated** - Year when house was renovated
* **zipcode** - zip
* **lat** - Latitude coordinate
* **long** - Longitude coordinate
* **sqft_living15** - The square footage of interior housing living space for the nearest 15 neighbors
* **sqft_lot15** - The square footage of the land lots of the nearest 15 neighbors

## Assumptions
### 1. Unused Data
Since the project is specifically targeted toward house prices in the King County area, I would be dropping some columns from the dataset to reduce the complexity of the model;
1) **id**
2) **date**
3) **lat**
4) **long**

### 2. Renovated Houses
To simplify the task, I have converted data for yr_renovated into a boolean. For future works, we should include the time between the last renovation and the time of sale.

### 3. Identifying Categorical Variables
Since some variables (i.e number of Bedrooms, Bathrooms, etc) in the dataset seem to be numeric but they take on values from a limited set of possibilities,
we shall identify them as Categorical Variables.

**Categorical variables:**
1) Bedrooms
2) Bathrooms
3) Floors
4) Waterfront
5) View
6) Condition
7) Grade
8) Renovated

## Feature transformations
### 1. One-hot Encoding
Even though the variables we identify as categorical are in integers (i.e. ‘bedrooms’), the number of possible values is limited to a fixed set.
With one-hot, we convert each categorical value into a new categorical column and assign a binary value of 1 or 0 to those columns. Each integer value is represented as a binary vector.

### 2. Log-Transform & Homoscedascity Check
Homoscedasticity occurs when the variance in a dataset is constant, making it easier to estimate the standard deviation and variance of a data set. 

Homoscedasticity is a key assumption for employing linear regression analysis. To validate the appropriateness of a linear regression analysis, homoscedasticity must not be violated outside a certain tolerance.
Hence, all continuous variables shall undergo log transformation and check for homoscedasticity.

### 3. Feature Scaling
Having features so different in magnitude will also affect the output and not only the learning process since features with larger magnitudes weigh more in the model.
Hence, all continuous variables shall undergo feature scaling to match the scale of each other and the scale of the categorical variables.

## Building the Model
After exploring and preprocessing the data, several iterations of multiple linear regression models were built in OLS, with price as the dependent variable.
Model iterations focus on eliminating high multicollinearity features using VIF score and removing non-significant features by identifying columns with high P-value. 

**Model 1**

 Model 1 acts as a baseline model.
OLS Regression Results show features with high P-values.
VIF score of Model 1 shows features with high VIF value indicating high multicolinearity.

We will be going back and forth between these two values to drop features with low statistical significance
and to reduce the multicollinearity of features.

**Model 2**

From the previous model, we dropped 'grade_7' due to its very high VIF score.
We can see it does not affect the R-squared value of the OLS model.
But significantly changes the VIF score of all other features.

From here we continue dropping features according to their P-value and VIF score

**Model 3**

Finally, we arrived to Model 3.
We have dropped multiple features since and have been able to remove all low-significant features.
We also managed to heavily reduce the VIF score of all available features in the model.
By removing certain columns, we noticed that the R-squared value of the model has slightly dropped meaning we sacrificed a small model accuracy in favor of eliminating colinearity among predictors.

With those assumptions satisfied, Model 3 is picked as our final model.

## Final Model
### 1. Normality Check
A normally distributed residuals are necessary for estimating accurate standard errors for the model parameter estimates.
We will check the distribution of residuals using a histogram and QQ plot.

![image](https://github.com/FooZheShen/KC_house_price_prediction_using_ML/assets/153910230/8dbfe25b-882e-4427-90f1-911fc473fa5b)
![image](https://github.com/FooZheShen/KC_house_price_prediction_using_ML/assets/153910230/a45d6d69-6605-49e3-a927-ab0c7d219a9a)

Almost all points fall along the QQ line. 
This shows the points have little to no deviations from the gradient.

Hence, residuals from Model 3 are normally distributed and satisfy the normality assumptions.

## 2. Model Testing and Validation
![image](https://github.com/FooZheShen/KC_house_price_prediction_using_ML/assets/153910230/27e10cf1-2433-4404-b370-ce4d3dde43a8)


![image](https://github.com/FooZheShen/KC_house_price_prediction_using_ML/assets/153910230/65f1d83a-29c6-4d2f-8302-6304d00e9009)

The plot above shows the residuals (differences between the predicted and actual price) against the predicted values. 
A well-performing model will have residuals scattered randomly around zero (the red dashed line).

## Results 
The results show the R-squared and its adjusted value of the train and test data;

* R-squared for train: 0.6033651270434894
* R-Squared for test: 0.5898111024076923
* Adjusted R-Squared for test: 0.6025143215779707
* Adjusted R-squared for train: 0.5877521150001701
* R-squared for train and test data accounts for about 60.3% and 58.9% respectively.
* Adjusted R-squared for train and test data accounts for about 60.2% and 58.7% respectively.

Both train and test sets are very close.
Hence, the final model can predict house prices with an accuracy of nearly 60% when fitted with new data.

## Conclusion
From the model, we gather;

Features that impact house price prediction in King County:
1. The size of the living space and basement ('sqft_living & sqft_basement')
2. The number of bedrooms and bathrooms
3. The grade of the house.
4. House condition.
5. The view the property has.
6. If the house was renovated before.
7. If the house is close to water.

**Limitations of the Model:**

For this model, we did not address how much time the house has since been renovated, and thus any recent renovations that may impact the price were not considered. 

Given that some of the features needed to be log-transformed to satisfy regression assumptions, 
new data used with the model would have to undergo similar preprocessing. 

Additionally, the model was built on a dataset solely belonging to the region of King County, the model's applicability to data from other counties may be limited. 

Furthermore, some outliers were removed, when fitted with new values, the model may also not accurately predict extreme values.

**Future works:**

Future models could include an interaction variable of date built and date renovated.
Additionally, we can also explore the long and lat of houses to discover the actual distance from water and how prices may be affected. 


 
