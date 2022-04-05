# Michelin Map

## Introduction

Starting in 1926, the first Michelin Star ratings (one star) were awarded to restaurants if they were deemed a “fine dining establishment.” They were all located in France. In 1931, the rating system was expanded to become the Michelin three-star rating that it continues to be today. The Michelin star rating didn’t take hold in America until 2005, and concentrated solely on fine dining in New York at the time. Today, the Michelin Guide reviews restaurants in select U.S. cities including Chicago, New York, Los Angeles, Las Vegas, and San Francisco. 

### Purpose

The Michelin reviewers, also known as Inspectors, keep their identities a secret to visit restaurants and have their meals expensed by Michelin (the restaurants do not pay for their meals). The Michelin Guide goes above and beyond to protect the anonymity of their Inspectors (they are not allowed to disclose their line of work to anyone outside Michelin). Due to the high volume of restaurants existing, it would be impossible for inspectors to visit each one to determine whether it is Michelin-worthy or not. With this existing gap, we decided to build a machine learning model.

### Our Questions

1. Could Yelp data and reviews help predict how many stars a known Michelin restaurant has?
2. Could Yelp data and reviews help predict if a given restaurant has any number of Michelin stars or not?

## Data

### Source Data
To build our models, we wanted to be able to pull as much data as possible to optimize machine learning. After reviewing various food data sites, we chose a dataset from [Kaggle for Michelin star restaurant data from 2019](https://www.kaggle.com/datasets/jackywang529/michelin-restaurants). We also gathered additional restaurant data using a Yelp API, and scraped Michelin restaurant data from Yelp using BeautifulSoup and Splinter.

Reasoning:
- Most robust data tables
- Longest history of data
- Low level of complexity on the Yelp website, allowing us to scrape without a web driver (Jupyter Notebook)

#### Initial Overview of Michelin Dataset

<p align="center">
  <img width="500" alt="Michelin Restaurants by Region" src="https://user-images.githubusercontent.com/15335096/161188446-31a10b62-b47c-4f4f-981f-c1e21a085615.png"><img width="500" alt="Michelin Restaurants by # of Stars" src="https://user-images.githubusercontent.com/15335096/161190047-c83d00db-b21f-4e91-a835-c157f083fa87.png">

  <img width="1047" alt="Michelin Restaurants by Star and Cuisine" src="https://user-images.githubusercontent.com/15335096/161189771-03cd3fa8-77b8-4e80-9bf8-545c2821e14a.png">
</p>

### Data Cleaning
The data was cleaned and merged using Jupyter Notebook. We created two datasets:
1. [Dataset of 179 Michelin star restaurant data with their corresponding Yelp data](Resources/michelin_ML.csv)
2. [Dataset of ~7,000 Yelp restaurant reviews, including the Michelin star restaurants from the first dataset](Resources/combine_data.csv)

### Data Storage
The datasets were stored in CSV files and SQLite databases.

## Machine Learning Models

### Building the Models
We tested several different types of models. We split the data into training and testing sets as appropriate.

To answer our first question, _Could we predict how many stars a Michelin Starred restaurant has?_ We started with a Linear Regression model and a SVC model with little success and moved onto a Deep Learning model. An accuracy score of 84% was obtained.

To answer our second question, _Could Yelp data and reviews help predict whether a restaurant has a Michelin star?_ We at first used Random Forest, Logistic Regression, and a Deep Learning Model. All three models came to the same result, and had an overall accuracy score of 97%, with very high accuracy in predicting if a restaurant did not have a Michelin star, and extremely low accuracy in predicting if it did have one. We then used Resampling Models (Oversampling, Undersampling, Combination, Balanced Random Forest, and Easy Ensemble AdaBoost).

### The Models

![2](https://user-images.githubusercontent.com/92230478/161401312-4b49bec3-8c14-4c11-8f76-15699386b87b.PNG)

* The confusion matrix shows that our model was the most accurate for properly classifying 1 star restaurants with 97.4% accuracy
  * 2 star accuracy: 9.1%
  * 3 star accuracy: 0%
* However, this model has predicted that 49 out of the 54 restaurants given had only 1 star.
* We can conclude from this that the 72% accuracy is not actually indicative of a successful machine learning model but instead the result of feeding the model a dataset with too few rows of data and an imbalanced ratio of 1, 2, and 3 starred restaurants (as shown in the figure on slide 8). 
This model is a poor predictor of how many stars a Michelin starred restaurant has received. 


![Capture1](https://user-images.githubusercontent.com/92230478/161401283-753dfedd-acc3-4e4d-aa6e-4917fae1bdb9.PNG)

* Input features included: 'review_count', 'rating', 'price', 'latitude', 'longitude'
* Our model has an accuracy score of 0.84 which indicates some relevance of the Yelp data in determining how many stars a known Michelin starred restaurant has.
* Although, it should be noted that in our dataset about 77% of the restaurants had 1 Michelin star. It is possible that this high ratio of 1 star restaurants is partially responsible for the 84% accuracy in our model.


![3](https://user-images.githubusercontent.com/92230478/161401364-f177c232-bf18-4acb-898e-2e0ad2d2a504.PNG)

* Using a Deep Learning Model, there was very little difference in changing the features. The only features that made a significant difference in importance was ‘price’ and ‘stars’. 
* The Deep Learning Model Accuracy score continuously produced a 97% accuracy rate, and we realized that the model was predicting a 97% accuracy of restaurants that did not have a Michelin star, rather then predicting the ones that did. This ended up being similar to our example from one of our course modules of a model that more accurately predicts a legitimate credit card charge, than accurately predicting a fraudulent credit card charge. 
* We had similar results when utilizing a Logistic Regression Model, as well as a Random Forest Model. 
* We then switched to use a supervised machine learning model to see if we could get a model to predict the whether a restaurant was a Michelin Star Restaurant. 
* In using the Naive Random oversampling, oversampling, a combination of over and under sampling, balanced random forest classifier, and easy ensemble Adaboost classifier models, they all had a similar result, where with our test and training data, the models predicted with 100% precision whether a restaurant had a star or not. 

![4](https://user-images.githubusercontent.com/92230478/161401385-acfc559e-ba24-4a6c-9aaa-5f0c8145e801.PNG)

* In using the Naive Random oversampling, oversampling, a combination of over and under sampling, balanced random forest classifier, and easy ensemble Adaboost classifier models, they all had a similar result, where with our test and training data, the models predicted with 100% precision whether a restaurant had a star or not. 
* While we want a model that achieves a high accuracy or precision score, this was almost too perfect. 
* These models correctly classified a Michelin Star restaurant and non-Michelin star restaurants every time. It did not matter which features we used. 
* This is most likely a result of Overfitting. The model learned the detail in the training data, ours may be too specific, and impacts the performance. In this case, accurately predicts it every time.
* In trying to fix the overfitting, we had tried removing features and using more data, but came up with the same result. If given more time, we could try other techniques in order to try and fix the overfitting, but the dataset that we chose is just so specific, that it hypertuned our results. 


## Conclusion
First Question: Can we accurately predict how many stars a Michelin starred restaurant has using data from Yelp?
* The Logistic Regression and Support Vector Classification Models were unsuccessful predictors of our first question. Although we yielded an 84% accuracy with the Deep Learning model, our dataset was far too small and we did not find meaningful results. 

Second Question: Could Yelp data and reviews help predict whether a restaurant has a Michelin star?
* Using various models of both Supervised and Unsupervised Machine Learning Models to determine whether machine learning can predict if a restaurant has a Michelin Star, we found that Deep Learning and Undersampling were the least accurate models, while all Supervised Machine Learning models were very precise in determining Michelin Star restaurants.

### Next Steps

Improving the Model:

* Include more restaurants with Michelin stars into the dataset, which would require expanding to additional countries (179 restaurants from the United States included in dataset, with only roughly 200 Michelin star restaurants in the US at a given time).
* Include more data from Yelp: scraping Yelp reviews and using Natural Language Processing to extract and analyze keywords andsorting Yelp reviews into elite and regular members to see if reviewer status has an impact on predicting if a restaurant is Michelin starred

Continued Testing of Accuracy:
* Since the Michelin star restaurant data used in this analysis was from 2019, we could compare and improve the model against known 2020-2021 Michelin star restaurant data.

Future Models
* Make year 2020-2022 predictions and compare to real results.

## Summary
[Google Slides Project Overview]('Michelin Stars & Yelp Ratings.pdf')

[Tableau visualizations](https://public.tableau.com/views/MichelinRestaurantsbyStarandCuisine/Sheet1?:language=en-US&publish=yes&:display_count=n&:origin=viz_share_link)
