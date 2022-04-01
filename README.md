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

**Initial Overview of Michelin Dataset**

<p align="center">
  <img width="500" alt="Michelin Restaurants by # of Stars" src="https://user-images.githubusercontent.com/15335096/161186391-f3d2ac60-2d1c-4714-a49d-92fb08f84e46.png"><img width="500" alt="Michelin Restaurants by Region" src="https://user-images.githubusercontent.com/15335096/161186400-7fd1543a-06d1-45d0-9808-4f98aea3fb07.png">
  <img width="800" alt="Michelin Restaurants by Star and Cuisine" src="https://user-images.githubusercontent.com/15335096/161186410-805a5df9-73da-4aac-a0dd-f71834777f66.png">
</p>

### Data Cleaning
The data was cleaned and merged using Jupyter Notebook. We created two datasets:
1. [Dataset of 179 Michelin star restaurant data with their corresponding Yelp data](Resources/michelin_ML.csv)
2. [Dataset of ~7,000 Yelp restaurant reviews, including the Michelin star restaurants from the first dataset](Resources/combine_data.csv)

### Data Storage
The datasets were stored in CSV files and SQLite databases.

## Machine Learning Models

### Building the Models
We tested several different types of models.

To answer our first question, _Could we predict how many stars a Michelin Starred restaurant has?_ We started with a Linear Regression model and a SVC model with little success and moved onto a Deep Learning model. An accuracy score of 84% was obtained.

To answer our second question, _Could Yelp data and reviews help predict whether a restaurant has a Michelin star?_ We at first used Random Forest, Logistic Regression, and a Deep Learning Model. All three models came to the same result, and had an overall accuracy score of 97%, with very high accuracy in predicting if a restaurant did not have a Michelin star, and extremely low accuracy in predicting if it did have one. We then used Resampling Models (Oversampling, Undersampling, Combination, Balanced Random Forest, and Easy Ensemble AdaBoost).

### What Worked
**Neural Network Model to Determine 1, 2, or 3 Michelin Stars**

![NNM to Determine 1,2,3 Michelin Stars - loss accuracy](https://user-images.githubusercontent.com/15335096/161188060-9e4c8d75-b906-4811-9dda-f562181bf377.png)

![NNM to Determine 1,2,3 Michelin Stars - graph](https://user-images.githubusercontent.com/15335096/161187983-cc0e7d4a-272e-40a1-991c-6f76b284b43a.png)


The Undersampling model accurately predicts 45 restaurants have Michelin Stars.

### What Didn't Work

## Summary
[Google Slides](https://docs.google.com/presentation/d/1rlgLjCL67ObVTJGFYM0-nu0BmKD3xxvakFf2mfFInd4/edit?usp=sharing)

[Tableau visualizations](https://public.tableau.com/views/MichelinRestaurantsbyStarandCuisine/Sheet1?:language=en-US&publish=yes&:display_count=n&:origin=viz_share_link)
