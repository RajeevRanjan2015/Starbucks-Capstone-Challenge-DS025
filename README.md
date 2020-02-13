# Starbucks-Capstone-Challenge-DS025

I chose this as my capstone project for Data Scientist Nanodegree offered by Udacity.

## Table of Contents:
1. Project motivation
2. Installation 
3. Data set
4. File/data description
5. Data preparation
6. EDA
7. Result
8. Conclusion

## Project Motivation:

I chose this project to understand the success rate of offers being sent and analysis is done through addressing the following questions.

1. How many customers were provided with a specific offer?
2. What's the performance level of an offer?

## Installation:

For running this project, the most important library is Python version of Anaconda Distribution. It installs all necessary packages for analysis and building models.

You may require to install progressbar library.
    conda install progressbar
    
## Data Set:

This data set contains simulated data that mimics customer behavior on the Starbucks rewards mobile app. Once every few days, Starbucks sends out an offer to users of the mobile app. An offer can be merely an advertisement for a drink or an actual offer such as a discount or BOGO (buy one get one free). Some users might not receive any offer during certain weeks.
Not all users receive the same offer, and that is the challenge to solve with this data set.

Your task is to combine transaction, demographic and offer data to determine which demographic groups respond best to which offer type. This data set is a simplified version of the real Starbucks app because the underlying simulator only has one product whereas Starbucks actually sells dozens of products.

Every offer has a validity period before the offer expires. As an example, a BOGO offer might be valid for only 5 days. You'll see in the data set that informational offers have a validity period even though these ads are merely providing information about a product; for example, if an informational offer has 7 days of validity, you can assume the customer is feeling the influence of the offer for 7 days after receiving the advertisement.

You'll be given transactional data showing user purchases made on the app including the timestamp of purchase and the amount of money spent on a purchase. This transactional data also has a record for each offer that a user receives as well as a record for when a user actually views the offer. There are also records for when a user completes an offer.

## Data Description:

The data is contained in three files:

    portfolio.json - containing offer ids and meta data about each offer (duration, type, etc.)
    profile.json - demographic data for each customer
    transcript.json - records for transactions, offers received, offers viewed, and offers completed
   
Here is the schema and explanation of each variable in the files:

#### portfolio.json

    id (string) - offer id
    offer_type (string) - type of offer ie BOGO, discount, informational
    difficulty (int) - minimum required spend to complete an offer
    reward (int) - reward given for completing an offer
    duration (int) - time for offer to be open, in days
    channels (list of strings)
    
#### profile.json

    age (int) - age of the customer
    became_member_on (int) - date when customer created an app account
    gender (str) - gender of the customer (note some entries contain 'O' for other rather than M or F)
    id (str) - customer id
    income (float) - customer's income
    
#### transcript.json

    event (str) - record description (ie transaction, offer received, offer viewed, etc.)
    person (str) - customer id
    time (int) - time in hours since start of test. The data begins at time t=0
    value - (dict of strings) - either an offer id or transaction amount depending on the record

## Data Preparation:

There are three datasets provided and each dataset is cleaned and preprocessed for further analysis. The target features for analysis are offer_success, percent_success.

   Portfolio - renaming id column name to offer_id, one-hot encoding of channels and offer_type columns
   Profile - profile: renaming id column name to customer_id, replacing age value 118 to nan, creating readable date format in became_member_on column, dropping rows with no gender, income, age data, converting gender values to numeric 0s and 1s, adding start year and start month columns (for further analysis)
   Transcript - renaming person column name to customer_id, creating separate columns for amount and offer_id from value col, dropping transaction rows whose customer_id is not in profile:customer_id, converting time in hours to time in days, segregating offer and transaction data, finally dropping duplicates if any
 
 
 ## EDA (Exploratory Data Analysis):
 
It is the most important phase of any data science project as we go more deeper into data to understand it better statistically and that helps in making decisions that what should to be followed going further.

#### How many customers were provided with a specific offer?
     Offer success rate (percent success):
     
     <img src="https://github.com/RajeevRanjan2015/Starbucks-Capstone-Challenge-DS025/blob/master/EDA1.PNG">
   
     
     

 
 
 ## Result:
 
 Results suggest that a random forest model's accuracy and f1-score is better than the naive predictor
 
    1. Accuracy
         Naive predictor: 0.471
         Random forest: 0.762
    2. F1-score
       Naive predictor: 0.640
       Random forest: 0.753
       
NOTE: Few things to consider while constructing these models - all features were converted to numericals to fit and train above models. Bias and variance are two characteristics of a machine learning model. Bias refers to inherent model assumptions regarding the decision boundary between different classes. On the other hand, variance refers a model's sensitivity to changes in its inputs. These can influence our results sometimes so models have to be tested throughly against bias and variance. Also, while splitting train and test datasets and tuning parameters to fit a model, we will have to make sure that data doesn't overfit the model.     
       
 ## Conclusion:
 
The problem that I chose to solve was to build a model that predicts whether a customer will respond to an offer. My strategy for solving this problem has mainly two steps. First, I combined offer portfolio, customer profile, and transaction data. Second, I assessed the accuracy and F1-score of a naive model that assumes all offers were successful. Third, I compared the performance of logistic regression and random forest models. This analysis suggests that a random forest model has the best training data accuracy and F1-score. Analysis suggests that random forest model has a training data accuracy of 0.762 and an F1-score of 0.753. The test data set accuracy of 0.740 and F1-score of 0.730 suggests that the random forest model I constructed did not overfit the training data.

However, the performance of a random forest model can be still improved by analysing features which impacts an offer’s success rate as a function of offer difficulty, duration, and reward. These additional features should provide a random forest classifier with the opportunity to construct a better decision boundary that separates successful and unsuccessful customer offers.

Also, initially it seemed like we had a lot of data to work, but once NaN values and duplicate columns were dropped and the data were combined into one single dataset, it felt as though the models might have benefited from more data. With more data, the classification models may have been able to produce better accuracy and F1-score results.

Additionally, better predictions may have been deducted if there were more customer metrics. For this analysis, I feel we had limited information about customer available to us — just age, gender, and income. To find optimal customer demographics, it would be nice to have a few more features of a customer. These additional features may aid in providing better classification model results.
