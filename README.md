Hotel Dataset 

Problem Statement: 

The data is from one of the world’s largest online travel agencies (OTA) which powers search results for millions of travel shoppers every day.  

In this competitive market matching users to hotel inventory is very important since users easily jump from website to website. As such, having the best ranking of hotels (“sort”) for specific users with the best integration of price competitiveness gives an OTA the best chance of winning the sale. 

The dataset includes shopping and purchase data as well as information on price competitiveness. The data are organized around a set of “search result impressions”, or the ordered list of hotels that the user sees after they search for a hotel on the agency's website. The user response is provided as a click on a hotel or/and a purchase of a hotel room. 

To predict if the user chooses a hotel based on the users’ browsing history from search to bookings and payments. 

Exploratory Data Analysis and Data Pre-processing: 

All the missing values have been handled by replacing with: 

median if the feature is skewed 

mode if it contains categorical data  

mean if it follows normal distribution 

Data Sampling and Normalization: 

Used Stratified split to select 1% of the data from the original dataset and to ensure the class balance is kept intact. 

Normalized the features which had higher range to bring it to a uniform scale. 

Model details 

I have choosen logistic regression model as the class variable is categorical in nature. Initial model was ran by considering all the parameters. This resulted in a low f1 score. Hence feature selection and hyper parameter tuning was applied to increase the score. 

Feature selection 

1. Used corr() for detecting multicollinearity among features. 

In case of multicollinearity, we might lose reliability in determining the effects of individual features in the model and hence, we remove these features. 

To resolve this, we use corr() method which returns a correlation score for each feature.   

This score determines the strength of correlation between the independent variables. All the features with a score greater than 0.50 were removed from the dataset suggesting high multicollinearity. 

The following features: search_id, listing_id and time_stamp, booked are irrelevant and hence have been removed. 

Model Building and Hyperparameter tuning 

1. Choosing the right predictor variable: 

Out of the 3 possible outcome variables: clicked, bookings_value and booked. I chose "clicked" as the outcome variable for my model considering the following reasons: 

Since, we are trying to predict whether the user is going to pick the hotel given multiple choices of hotels and competitors’ websites, the ideal choice would be to predict the maximum probability of a click (“clicked”) which indicates a visitor’s interest and potentially a decision to book. 

“Bookings_value” does not apply here since it does not address the problem statement in hand, our goal is not price prediction rather if the user is going to pick a hotel given multiple choices of hotels and competitor’s websites. 

The outcome variable "Booked" would come into picture when we are trying to predict if the user is going to book a particular hotel or not given a single website/source. In our case, we are also trying to compare between different websites, hence the outcome variable "Booked" is not applicable here. 

2. Machine Learning algorithm used: 

Applied "Cost Sensitive/Weighted Logistic Regression" taking into consideration the following reasons: 

Predicted variable is categorical 

Class has imbalanced data: The dataset has imbalanced class with approximately:  

94% - negative class and 6% - positive class because of which the accuracy metrics get inflated. This has been handled by considering the metric "F1 score" while tuning hyper parameters and measuring the success of the model. 

3.Hyperparameter Tuning: 

Applied GridSearchCV to fetch optimum values for weights and alpha. 

Used Kfold cross validation to ensure we are not overfitting the model. 

4.Selection of significant features: 

Used RFE algorithm to find out significant features for the model and removed insignificant features. 

5. Evaluation metrics: 

I chose “average f1 score” to evaluate the accuracy of the model and also to tune the hyper parameters of the model. 

Since we are predicting class labels and both false negatives and false positives are equally costly, we use the F1 measure as the evaluation metric for our model.          

Conclusions: 

I achieved a model f1-score of 89%. Click through rate and conversion rate have been calculated for different levels of property stars and property review score for the test data.  

 
