# Scalable ETL Pipeline Predicting Dogecoin Stock Performance using Twitter Data

- Collected Twitter data containing Dogecoin, preprocessed using Spark and stored in MongoDB. 
- Utilized different Machine Learning models (Linear Regression, Random Forest, AutoML) to analyze the impact of tweets on Dogecoin’s stock price  
# Table of Contents
1. [Description of data and data collection process](#description-of-data-and-data-collection-process)
2. [Analytical goals](#analytical-goals)
    1. [Tweets Count](#tweets-count)
    2. [Features of Tweets](#features-of-tweets)
    3. [Sentiment of Tweets](#sentiment-of-tweets)
4. [Findings](#findings)
5. [Conclusion](#conclusion)


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
     

## Analytical goals
### Tweets Count
__Predict the daily stock price given the number of tweets on a given date (tweets volume)__

Model Used: Linear Regression, Random Forest

[The link to the notebook is here]()

### Features of Tweets
Analytical Goal: Add retweet, reply, comment, like counts as features and predict price (y = daily stock price)
![Goal2](https://github.com/TinaLiu46/Predicting-Dogecoin-Stock-Performance-using-Twitter-Data/blob/main/Images/Goal2.png?raw=true "Title")

### Sentiment of Tweets
Analytical Goal: Add text sentiment score into the model and predict the daily stock price
![Goal2](https://github.com/TinaLiu46/Predicting-Dogecoin-Stock-Performance-using-Twitter-Data/blob/main/Images/goal3.png?raw=true "Title")
## Findings
## Conclusion

<h3 align="left">Connect with me:</h3>
<p align="left">
</p>

<h3 align="left">Languages and Tools:</h3>
<p align="left"> <a href="https://aws.amazon.com" target="_blank" rel="noreferrer"> <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/amazonwebservices/amazonwebservices-original-wordmark.svg" alt="aws" width="40" height="40"/> </a> <a href="https://www.mongodb.com/" target="_blank" rel="noreferrer"> <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/mongodb/mongodb-original-wordmark.svg" alt="mongodb" width="40" height="40"/> </a> <a href="https://pandas.pydata.org/" target="_blank" rel="noreferrer"> <img src="https://raw.githubusercontent.com/devicons/devicon/2ae2a900d2f041da66e950e4d48052658d850630/icons/pandas/pandas-original.svg" alt="pandas" width="40" height="40"/> </a> <a href="https://www.python.org" target="_blank" rel="noreferrer"> <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/python/python-original.svg" alt="python" width="40" height="40"/> </a> <a href="https://scikit-learn.org/" target="_blank" rel="noreferrer"> <img src="https://upload.wikimedia.org/wikipedia/commons/0/05/Scikit_learn_logo_small.svg" alt="scikit_learn" width="40" height="40"/> </a> </p>
