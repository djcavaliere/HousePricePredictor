### Project 2 - Ames Housing Data and Kaggle Challenge

Background:
You are tasked with creating a regression model based on the Ames Housing Dataset. This model will predict the price of a house at sale. The Ames Housing Dataset is an exceptionally detailed and robust dataset with over 70 columns of different features relating to houses.

Approach & Repo Organization:
1) Notebook 1: EDA and Data Cleaning
2) Notebook 2: Feature Engineering
3) Notebook 3: Build, Evaluate, and Iterate Model

# Data Overview & Summary:
The data provided is broken into two sets. The first set is the training data which contains 2051 rows, 79 features and 1 target variable which is the Sale Price of homes in Ames, Iowa. The dataset spans home sales from 2006-2010 and below are some summary statistics for the Sale Price target variable: 

|Attribute|Amount|
|---|---|
|mean|181,469|
|std|79,258|
|min|12,789|
|25% Quartile|129,825|
|50% Quartile|162,500|
|75% Quartile|214,000|
|max|611,657|

Correlation:
One of the key principles of building a successful linear regression model is identifying feature variables that demonstrate significant correlation with the target variable. In analyzing the relationship between the feature and target variables I identified the following variables with the highest correlation with Sale Price (Overall Quality, Square Feet, Bedrooms, Garage Cars, Year Built) These features will be key to emphasize within our model in order to generate the most accurate predictions.

Outliers:
![Scatters](https://git.generalassemb.ly/dcavaliere/project-2/blob/master/img/scatters.png)

In the Scatter Plots above I identified two outlier homes that could potentially adversely impact the accuracy of our model. As you can see in the lower right hand corner of our square feet to price plots there are two homes with exceptionally large square footage but relatively low Sale Prices. After removing these two outliers our model should fit a more accurate line through the dataset.


# Feature Engineering:
New Features- As part of my feature engineering efforts I created two new features one column 'HouseSF' which totals all of the square footage for each home into one column and another column 'Baths' which totals all of the full and half baths for each home. I created these two columns because homes are typically priced based on total square feet and home buyers typically consider total number of bedrooms and baths when searching and making their purchase. 

Dummy Features- The dataset included many categorical variables which cannot be read by a linear model as only numerical columns can be fed into the model. As such I dummified all the categorical features into 1's and 0's dropping the first dummified column as the baseline for comparison. 

Polynomial Features- Lastly I created Polynomials of Square Feet, Bedrooms, Bathrooms, Overall Quality as I believe these featuers have strong correlation with the target variable and the interaction between them is highly valued by buyers.

# Model Build and Evaluation
Baseline- Taking the mean SalePrice of the training data to predict the SalePrice resulted in an RMSE of $79k. This will serve as the baseline which we can compare each model to judge improvement from simply using the average.

Basic Model- In my first model I simply fit a linear regression model with six features that showed strong correlation with the target variable. These six features included Overall Qual, Gr Liv Area, Garage Area, Lot Area, TotRms AbvGrd, Bedroom AbvGr.

Model 2- The next model I built was slightly more complex as I added all of my engineered features pushing the complexity from 6 features to 204 features. As seen below this drew significant improvement in the models ability to predict the target variable.

Model 3- In this model I scaled all 204 features using StandardScaler and fit these features into a LassoCV Regression model. Ultimately this model saw the best performance as demonstrated below.

|Model|RMSE|
|---|---|
|Baseline|79,012|
|Model1|36,539|
|Model2|24,589|
|Model3|24,464|

In this exercise we are trying to optimize the model by reducing the Root Mean Square Error (RMSE) as much as possible. For this project the RMSE represents the average difference between our predicted sale price and the actual sale price of the test data. As shown above the final model, Model 3, performed the best predicting on average +-24,464 of the true Sale Price.

# Conclusions and Recommendations
In conclusion we built a LassoCV regression model that can predict the Sale Price of a home in Ames, Iowa within +-24,464 dollars. Further, if a prospective seller wants to increase the value on their home I would recommend focusing firstly on increasing the overall quality score and secondly on increasing the square footage based on my analysis of the correlation between features and target.
