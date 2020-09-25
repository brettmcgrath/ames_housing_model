## Table of Contents  
- [Project Contents](#Project_Contents)
- [Data](#Data)  
- [Data Problem](#Data_Problem)  
- [Data Cleaning and Exploratory Data Analysis](#Data_Cleaning_and_Exploratory_Data_Analysis)  
- [Preprocessing and Modeling](#Preprocessing_and_Modeling)  
- [Reflections on the modeling process](#Reflections_on_the_modeling_process)  

## Project Contents:

The attached file contains one datasets directory, two notebooks and three CSV files which constitute my data cleaning, analysis, and modeling of the Ames, Iowa housing dataset. The contents are as follows:
1. **ames_cleaning** - A Jupyter Notebook containing my preliminary data diving, exploring, analysis, and manipulation of categorical variables into new, more useful forms
2. **ames_models** - A Jupyter notebook containing further analysis, feature engineering, and modeling of the Ames dataset
3. **test_predictions** - A CSV file containing the predictions of housing prices from my proposed model
4. **cleaned_ames_train_data** - A CSV file containing the training dataset cleaned and transformed in ames_cleaning
5. **cleaned_ames_test_data** - A CSV file containing the test dataset cleaned and transformed in ames_cleaning
6. **datasets directory** - A directory containing the two original CSV files for training and testing data

## Data

Data used in this project can be seen on [Kaggle](https://www.kaggle.com/c/ames-iowa-housing-louisville/data), and a data dictionary is available for view by [clicking here](http://jse.amstat.org/v19n3/decock/DataDocumentation.txt).

## Data_Problem

The task I have accomplished is to create a model that best predicts house prices in Ames, Iowa based on a variety of features. Many features of Ames dataset have strong linear relationships with our target variable (price) and because of this, I chose multiple linear regression as a predictive model for price. The resulting model accounts for 90% of variability and predicts prices within $22587.09 give or take of actual home sale price based on r-squared and root mean square error respectively and could easily be implemented for use by sellers and buyers of real estate in Ames, Iowa, provided updated information since 2010. The rising cost of real estate, inflation, and many other factors may weigh in to create a situation in which my model, however great for 2010, likely will not perform as well in market conditions of 2020.

## Data_Cleaning_and_Exploratory_Data_Analysis

A significant amount of time and effort was placed on the tedious task of accounting for missing data, cleaning, and reorganizing the dataset in appropriate was for linear regression. Null values in the data set were imputed, and in most cases dropped when they were categorical variables needing to be dummy encoded. New data was created to create overall categories to explain the more specific, individualized points of the dataset (ie. total indoor or outdoor square feet, bathroom totals, outdoor square feet, overall quality of materials, etc). In most cases, the generalized data created had high predictive power and was linearly related to the target variable price, but most of these were not as strong predictors as using the individual variables describing individual parts of a home. The higher predictive power of these individual variables used together allowed me to conclude that not all square feet are equally as valuable in determining home price. 

## Preprocessing_and_Modeling

Careful time was spent researching feature interaction for linear relationships to the target variable as well as careful selection of variables based on their predictive power when found to be colinear with other variables. Features such as garage area and car ports were highly multicolinear as well as square footage above ground with total rooms. The final variables selected for modeling were:
* Total basement square footage
* Above ground square footage  
* Kitchen quality
* Exterior quality
* Neighborhood
* Basement quality
* Foundation type
* Basement finish state
* Garage type
* Garage area
* Fireplaces
* Cube root home age

A variety of models were analyzed, starting with multiple linear regression with a trial round of features. Models that are not included in these notebooks were attempted through a series of 6 different feature selection processes. Each model was tested with multiple linear regression using sklearn and subsequently tested with LassoCV, RidgeCV, including GridSearches for maximized hyperparameter tuning. Several scalers were attempted including: MinMaxScaler, minmax_scale, MaxAbsScaler, StandardScaler, RobustScaler, Normalizer, QuantileTransformer, PowerTransformer, PolynomialFeatures, all of which did not significantly improve, and in some circumstances hurt the r squared score of my models. I was happy to choose a RidgeCV regularized model with 0.904, 0.901 r squared score for training and testing score respectively. This model's target variable was cube-root transformed for optimal handling of the target variable right skew which improved the model's ability to account for variation over previous models. The nearly identical r-squared value for training and testing sets demonstrates this model's ability to perform outside of the data it was trained on for broader applicability on new Ames housing data. 

## Reflections_on_the_modeling_process

My baseline model performed well with a training r2 score of 0.917, cross validation r2 score if 0.905, and test r2 score of 0.899 and an RMSE of 27,140.18. The model didn't improve substantially, but did improve and compensate for the initial overfitting. The final model had an r2 value of 0.903 for training data and 0.901 for testing data. The RMSE of training data was $21,506.73, and $26,343.08 for testing data. 

## Conclusions_and_Recommendations

This model can be improved upon. The first thing I would do to improve upon my model is further examine outliers and see how to best deal with them. Though I explored polynomial features and decided they were not best for this model, I would like to explore if there are any polynomial features or interaction terms that improve model performance. The features selected for this model account for 90% of variability, so the features I have selected do well in predicting home prices and can be used (assuming no market change since) to plug in feature-specific information for homes on the market in Ames to determine an approximate fair selling or buying price.
