### Aimes housing data set

Introduction
In this project, my goal is to develop a regression model that will make accurate predictions of house prices in the city of Ames in Iowa, USA.

The benefits of obtaining accurate house price predictions are manifold.House owners can profit more from improving their fatures in their house and also the selling price of their house.

Through a regression model, we will also be able to identify some features that increase or decrease the value of a house. With this knowledge, property developers can better understand which features to include or exclude in future developments. They would already have domain expertise in this area, and a regression model could help to reinforce what they already know and perhaps reveal things that are less apparent.

The project involves analysing the Ames Housing Dataset, which is composed of over 2,900 records of properties transacted in Ames between 2006-2010. The 2,900 records are split between two separate train (2,051 records) and test (879 records) datasets.

Each instance comprises 78 features of four different data types: Nominal, Categorical, Continuous, and Discrete.

The target variable in our analysis is the SalePrice of the house.

To simplify my model, my aim will be to identify only the top 30 factors that influence the value of a house.

My work consists of two main components:

Data cleaning, preprocessing, and feature engineering
Modelling, feature selection, and prediction


### Part 1: Data cleaning, preprocessing, and feature engineering


Data cleaning
These were the steps taken to clean the data:

Drop columns with >80% missing values (four columns were dropped)
Observations with missing values were not dropped; instead I imputed values for them in a sensible manner
Remove features with low variance in their values as they would not help much in explaining the variations in SalePrice (around 90% or more of values in a single value)
Check the correlation between numerical variables and remove the highly correlated features
Remove features without meaningful information, e.g. MiscVal (unclear what information it contains) and LowQualFinSF (contains many 0 values and shows no relationship with SalePrice)

### Part 2: Modeling, feature selection, and prediction


After completing the data preparation phase, I started running the regression models to predict housing prices on holdout data from the train dataset.

Before training my models, I did a scaling of our feature variables so that they have a mean of 0 and standard deviation of 1. This helps to avoid the case where one or several features dominate others in magnitude, and as a result, the model hardly picks up the contribution of the smaller scale variables, even if they are strong.

Modeling
Four different models were tested using cross validation on training data:

ordinary least squares linear regression
ridge regression
lasso regression
elastic net regression
For my initial modelling step, I compared the performance of the 3 regularised linear models (Lasso, Ridge, and Elastic Net) with all 169 feature variables fitted onto them. OLS linear regression was not used as we still have a large number of features and that would result in severe overfitting.

Elastic Net performed the best in the initial modelling step, and to keep my process streamlined, I continued using the Elastic Net model to evaluate performance during feature selection.

### Conclusion
The Elastic Net model was able to perform consistently well (the mean CV R2 score remained around 0.89) even after cutting the number of features down.

The final model used to make predictions for the actual test dataset produced a CV mean R2 of 0.90169, which means the model was able to explain 90.2% of the variations in SalePrice. The Kaggle score (RMSE) was 23,267.

A disadvantage of using an Elastic Net model is that it would require more computational power since we also need to cross-validate the relative weight of L1 vs. L2 penalty, 𝛼. The scope of our analysis still allows us to run the Elastic Net model pretty swiftly, but for larger datasets with more instances and/or features, we might need to experiment with Lasso and/or Ridge instead.

Quantity/quality-related house features

As expected, a higher/better value in these features will almost always increase house value: TotalSF, OverallQual, OverallCond, TotalBath, LotArea, Fireplaces, GarageArea, BsmtFinType1, KitchenQual, HeatingQC, TotRmsAbvGrd, BsmtExposure, ExterQual, GarageQual.

A further investigation we can make is to check what finishings were used on houses with high OverallQual or ExterQual. Homeowners can select finishings with the best benefit-to-cost ratio to use on their houses when renovating, in order to bring about the greatest increment in SalePrice.

Physical attributes of the house

According to this model, BldgType_1Fam aka single-family detached houses will fetch higher prices than other types. A cross-reference to the boxplot of SalePrice against BldgType from our initial EDA showed us that there is a greater range of house prices associated with this building type, but that is only natural because most of the houses in our dataset are of this type (82.8%). We have to keep this in mind and avoid wrongly assuming that BldgType_1Fam properties will definitely have higher prices.

Houses with concrete (PConc) foundation are expected to have higher prices according to the model. This is not a conclusion we can make too quickly, as most houses in our dataset have a concrete foundation and we have limited instances with PConc foundation. This is a similar problem as described in point 3.

Exterior1st_BrkFace is positively correlated with SalePrice, suggesting that a brick facade is more popular in Ames.

Other features

It is common knowledge that location is a big determinant of a house's price. Neighborhood-wise, houses located in Crawfor, NridgHt and StoneBr are expected to fetch higher prices. Investing in undervalued houses in these neighborhoods will likely generate a positive return on investment.

Properties of classified as commercial buildings (MSZoning_C (all)), which are commercial buildings, are expected to have lower prices. Without knowing more details about those commercial properties in our dataset, it would not be wise to say that commercial properties are a poor investment in Ames.

HouseAge is negatively correlated with SalePrice, as is MSSubClass_30 (1-STORY 1945 & OLDER). Homeowners of older houses could remodel their houses before putting it up in the market for sale if they want to increase its SalePrice.

Limitations

Limited timeframe: Our data comprised only transactions between 2006–2010. This is a pretty short timeframe, which makes it hard to capture actual general trends in sale prices of houses in Ames. The housing market within the 2006-2010 timeframe could be very different from how it is in present time.


Limited generalisability to houses outside of Ames, Iowa: The predictive model we've built only applies to the houses in Ames and will not be accurate when applied to houses in other cities or countries. To make it more applicable across the board, we could perhaps remove features specific to houses in the U.S. or Ames, such as replacing Ames' neighborhood with a metric describing a property's distance from the city centre, or whether a property is near a buzzing commercial hub, etc.

© 2020 GitHub, Inc.
Terms
Privacy
Security
Status
Help
Contact GitHub
Pricing
API
Training
Blog
About



```python

```
