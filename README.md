# Predict-if-a-car-purchased-at-an-Auction-is-a-good-or-bad-buy

Objective: To build a classification model which should classify if a car purchased at an auction is a good/bad buy

Model Pipeline: 
Imputation of missing values -> Data Visualization & Manipulation -> Data Preprocessing -> Encoded Categorical features -> Standardization of features -> Imbalanced Class Handling -> Modeling (an ensemble of Random Forest, Gradient Boosting, XGBoost) -> Testing

Dataset Used: https://www.kaggle.com/c/DontGetKicked/data


Methodology Used:

1. Imputated the missing values or removed rows and columns if Nan values were significantly higher [I Data Cleaning - Training]
    I removed 'PRIMEUNIT' AND 'AUCGUART' attributes from the database because around 95.3% cells are filled with Nan values.
    I already had 'WheelTypeID' feature, so the categorical features: 'WheelType' was not required. Thus, removed it from the main dataframe.
    I filled NaN values of 'WheelTypeID', 'SubModel', 'Model', 'Trim' ,'Transmission', 'Nationality', 'Size', 'TopThreeAmericanName','Color' sophisticatedly using the rows. (Please refer: I Data Cleaning - Training)
    I removed 'Trim' feature when I was not able to fill NaN values using the above-mentioned approach.
    I filled the MMR features also very interestingly using linear regression. (Please refer: I Data Cleaning - Training)
    
2. Understanding Data - Data Visualization & Manipulation & Feature Engineering [II Understanding Data & Feature Engineering]
    I dropped 'VehYear' since I already had 'VehicleAge'.
    I also dropped 'RefId' (just a primary key).
    I started off with Univariate analysis of the features. I generated distribution/frequency plots. Some of the features like 'VehOdo','VehicleAge' have guassian distribution (which means data is internally consistent). 'WarrantyCost' has skewed distribution. MMR features displays similar characteristics. The remaining features don't exhibit any distribution. 
    Then, I did Bivariate analysis using box plot, correlation coefficient and observed that higher the vehicle's age, the more would be the probability of it being a bad buy.
    The MMR features are highly correlated to each other. And, MMR is correlated with VehBCost also.


3. Data Processing, Modeling & Testing [III Data Processing, Modeling & Testing]
    For Modeling, we needed to convert every categorical feature into numeric form. 
    I ordinally encoded these features for now(which might not be that effective). If I would have been given advanced features and top-of-the-line parts like 'enginer properties', 'braking system', etc. in correspondence with the model, submodel, that would have increased the accuracy of the model significantly. 

Factors affecting car longevity:
a. Advanced features & top-of-the-line parts 
b. Auto or Manual ('Transmission')
c. Wheel Type ('WheelTypeID')
d. Car Manufacturing company ('Nationality', 'TopThreeAmericanName') [According to a report, cars manufactured by Japanese companies are at the top of the list of higher life spans]
e. Advanced vehicle monitoring system


    The categorical features encoding was followed by standarization of features and feature selection using Gini Impurity.
    The dataset has 87.7% negative class and 12% majority class. There are several ways in which we can handle imbalanced classes: Random Under-sampling, Random Over-sampling and NearMiss. For this classification problem, we will be using Synthetic Minority Oversampling Technique (SMOTE).

    I trained the model using Logistic Regression, SVC, Random Forest, Gradient Boosting, XGBoost and AdaBoost and used Precision, Recall and F1 score as performance metrics. The best performing models are Random Forest, Gradient Boosting, XGBoost. Then, I used ensemble method using Random Forest, Gradient Boosting, XGBoost models. So, the main output is the 'mode' (statistics) of the outputs from these three models. 
    
4. Data Cleaning [IV Data Cleaning - Testing]
    I cleaned test dataset using similar technique as was used to clean training dataset. Then, after some pre-processing steps, I used the ensemble model to classify if a car bought is a good buy or not and have stored the result in 'test_output_file.csv'



Reference: https://0xreza.com/papers/dontgetkicked.pdf

