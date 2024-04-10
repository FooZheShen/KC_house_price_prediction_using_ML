# Predicting King County House Prices using ML
This report discusses the steps, procedures, assumptions, and validation methods used for my analysis.

## Introduction
For this project, I am tasked by the Real Estate Agency to identify key features of a home when trying to predict the house prices for future use 
when dealing with clients looking to sell or buy houses in King County.

I will be building a Multiple Regression Model to analyze and predict house sales in a northwestern county using the King County Sales dataset that has been provided.

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
When analyzing regression results, it's important to ensure that the residuals have a constant variance. I have taken steps to eliminate the skewness of the data as well as reducing biases due to value weight

### 1. Log-Transform & Homoscedascity Check
Homoscedasticity occurs when the variance in a dataset is constant, making it easier to estimate the standard deviation and variance of a data set. 

Homoscedasticity is a key assumption for employing linear regression analysis. To validate the appropriateness of a linear regression analysis, homoscedasticity must not be violated outside a certain tolerance.
Hence, all continuous variables shall undergo log transformation and check for homoscedasticity.

### 2. Feature Scaling
Having features so different in magnitude will also affect the output and not only the learning process since features with larger magnitudes weigh more in the model.
Hence, all continuous variables shall undergo feature scaling to match the scale of each other and the scale of the categorical variables.

## Building the Model
After exploring and preprocessing the data, several iterations of multiple linear regression models were built in OLS, with price as the dependent variable.

## Model Testing and Validation
## Results 
## Conclusion
From the model, we gather;

Features that impact house price prediction in King County:
1. The size of the living space and basement ('sqft_living & sqft_basement')
2. The number of bedrooms and bathrooms
3. The grade of the house.
4. House condition.
5. The view the property have
6. If the house was renovated before.
7. If the house is close to water.

Limitations of the Model: 
For this model, we did not address how much time the house have since been rennovated and thus any recent rennovations that may impact price were not considered. Further models could include an interaction variable of date built and date renovated.

Given that some of the features needed to be log-transformed to satisfy regression assumptions, 
new data used with the model would have to undergo similar preprocessing. 

Additionally, the model was built on a dataset solely belonging to the region of King County, the model's applicability to data from other counties may be limited. 

Furthermore, some outliers were removed, thus model may also not accurately predict extreme values.

Future Works
 
