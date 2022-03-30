# Scalable ETL Pipeline Predicting Dogecoin Stock Performance using Twitter Data

- Collected Twitter data containing Dogecoin, preprocessed using Spark and stored in MongoDB. 
- Utilized different Machine Learning models (Linear Regression, Random Forest, AutoML) to analyze the impact of tweets on Dogecoin’s stock price  
# Table of Contents
1. [Description of data and data collection process](#description-of-data-and-data-collection-process)
2. [Analytical Findings](#analytical-findings)
    1. [Analytical Finding 1](#analytical-finding-1)
    2. [Analytical Finding 2](#analytical-finding-2)
    3. [Analytical Finding 3](#analytical-finding-3)
3. [Conclusion & Lesson Learned](#conclusion-and-lesson-learned)


## Description of data and data collection process
Data Collection: 
- Ran script on AWS EC2 instance pulling related Tweets using API and stored data in __AWS__ S3 bucket
- Imported data from S3 to __Apache Spark__ for data preprocessing to create data aggregates on __Databricks__
- Stored the aggregates in MongoDB on __MongoDB Atlas__

      Data Size : 24036
      Date Range: 2020-01-01 – 2020-05-09
Examples of our dataframe is shown below:

| text  | retweet_count | reply_count  | like_count | quote_count  | created_date |
| ------------- | ------------- | ------------- | ------------- | ------------- | ------------- |
| Bitcoin going up sig...  | 0 | 1 | 0 | 2 | 2020-02-03 |
     

*The model runs on a cluster of 30.5 GB Memory, 4 Cores for both driver and workers, with # worker of 8

## Analytical Findings

### 🚀Analytical Finding 1
Analytical Goal: Explore the correlation of the daily stock price and the number of tweets on a given date (tweets volume)
- Model Performance: 
    - Linear Regression:

            R2: 0.06282
    - Random Forest

            R2: -0.1094

- Findings:

    Both the R^2 of test set of and Linear Regression and Random Forest < 0.1 - Tweets Counts and DogeCoin stock price are not significantly correlated.
- Possible Explanation:
    - The data we collected is not enough to generate some results
    - The fluctuation of stock price depends on so many factors - and tweets count is not important enough to explain this fluctuation.


The link to the notebook is here:[ Analytical Goal #1](https://github.com/TinaLiu46/Predicting-Dogecoin-Stock-Performance-using-Twitter-Data/blob/main/Notebooks/Analytical%20Goal%20%231.ipynb)

### 🚀Analytical Finding 2
Analytical Goal: Add retweet, reply, comment, like counts as features and predict price (y = daily stock price)
- Model Performance:
    - Random Forest:
        
            R2 score: 0.5115
            MSE: 0.05533
- Data Exploration
By looking at the distribution of features and the scatter plots, we find that our data was right skewed, which may lead to poor prediction result.
![Goal2](https://github.com/TinaLiu46/Predicting-Dogecoin-Stock-Performance-using-Twitter-Data/blob/main/Images/Goal2.png?raw=true "Title")
- Feature Engineering:

    We trained four random forest models to predict the stock price. The naive one without feature transformation got an extremely high R^2, which is counter-intuition. After taking the log, R^2 becomes negative.
- Possible explanation:

    It’s hard to tell why our data is right skewed. if it’s due to the rare market shock, then the high metric value from original model makes sense; if it’s due to outliers, the truncate one makes sense; if it’s due to lack of data, then the metric is not reliable

The link to the notebook is here:[ Analytical Goal #2](https://github.com/TinaLiu46/Predicting-Dogecoin-Stock-Performance-using-Twitter-Data/blob/main/Notebooks/Analytical%20Goal%20%232.ipynb)

### 🚀Analytical Finding 3
Analytical Goal: Add text sentiment score into the model and predict the daily stock price
- Sentiment Score Conversion Package
We used SentimentIntensityAnalyzer to convert cleaned text to a score converted score to a number between -1 and 1 (negative and positive)
- Models Performance:
    - RandomForestRegressor:

            RMSE: 0.3640
            MSE: ~0.1325
            R2: ~-0.0271
    - H2O:
    
            Best Model: StackedEnsemble_AllModels_4_AutoML_3_20220309_13719
            MSE: ~0.1165
            R2: ~0.1608
            Partial Dependence Plot: with many neutral sentiments, we still see negative sentiment tweets would yield to low stock closing price, vice versa.
![Goal2](https://github.com/TinaLiu46/Predicting-Dogecoin-Stock-Performance-using-Twitter-Data/blob/main/Images/goal3.png?raw=true "Title")
The link to the notebook is here:[ Analytical Goal #3](https://github.com/TinaLiu46/Predicting-Dogecoin-Stock-Performance-using-Twitter-Data/blob/main/Notebooks/Analytical%20Goal%20%233.ipynb)

## 💡Conclusion and Lesson Learned
- Different models could be used to explore different analytical goals; when we have more features, more time is required to do data cleaning and model fitting.
- Tweets Counts and DogeCoin stock price are not significantly correlated. (R2_RF : -0.11 ; R2_LR : 0.06)
- We notice some extremely validation metrics results when we add more features (reply count, like count,
quote count) to the model. Some of the possible reasons have been discussed before.
- When we take tweet sentiment into considerations, with the H2O model, only 16.1% of the variation was
explained. The sentiment score is making some influences on the stock price prediction, though limited. H2O would more likely to select the best model comparing to we individually implement one single model, as it could ensemble good models together.
- There might be many possible limitations in our dataset, e.g. right skewed data, limited amount, etc. Further investigations are required to build a better model. For future steps, we would like to gather more data and also include other possible features should be introduced.


<h3 align="left">Languages and Tools:</h3>
<p align="left"> <a href="https://aws.amazon.com" target="_blank" rel="noreferrer"> <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/amazonwebservices/amazonwebservices-original-wordmark.svg" alt="aws" width="40" height="40"/> </a> <a href="https://www.mongodb.com/" target="_blank" rel="noreferrer"> <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/mongodb/mongodb-original-wordmark.svg" alt="mongodb" width="40" height="40"/> </a> <a href="https://pandas.pydata.org/" target="_blank" rel="noreferrer"> <img src="https://raw.githubusercontent.com/devicons/devicon/2ae2a900d2f041da66e950e4d48052658d850630/icons/pandas/pandas-original.svg" alt="pandas" width="40" height="40"/> </a> <a href="https://www.python.org" target="_blank" rel="noreferrer"> <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/python/python-original.svg" alt="python" width="40" height="40"/> </a> <a href="https://scikit-learn.org/" target="_blank" rel="noreferrer"> <img src="https://upload.wikimedia.org/wikipedia/commons/0/05/Scikit_learn_logo_small.svg" alt="scikit_learn" width="40" height="40"/> </a> </p>
