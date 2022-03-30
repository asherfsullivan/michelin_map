# Michelin Map

## Introduction

Starting in 1926, the first Michelin Star ratings (one star) were awarded to restaurants if they were deemed a “fine dining establishment.” They were all located in France. In 1931, the rating system was expanded to become the Michelin three-star rating that it continues to be today. The Michelin star rating didn’t take hold in America until 2005, and concentrated solely on fine dining in New York at the time. Today, the Michelin Guide reviews restaurants in select U.S. cities including Chicago, New York, Los Angeles, Las Vegas, and San Francisco. 

### Purpose

The Michelin reviewers, also known as Inspectors, keep their identities a secret to visit restaurants and have their meals expensed by Michelin (the restaurants do not pay for their meals). The Michelin Guide goes above and beyond to protect the anonymity of their Inspectors (they are not allowed to disclose their line of work to anyone outside Michelin). Due to the high volume of restaurants existing, it would be impossible for inspectors to visit each one to determine whether it is Michelin-worthy or not. With this existing gap, we decided to build a machine learning model.

### Our Questions

- Can Yelp data and reviews help predict whether a restaurant has a Michelin star? Can we predict the number of Michelin stars a restaurant has by looking at their rating and/or review count from Yelp? 
- Using machine learning, can we predict which restaurants have gained a Michelin star since 2019? Can we predict into the future? 

## Data

### Source Data
To build our models, we wanted to be able to pull as much data as possible to optimize machine learning. After reviewing various food data sites, we chose a dataset from [Kaggle for Michelin star restaurant data from 2019](https://www.kaggle.com/datasets/jackywang529/michelin-restaurants). We also gathered additional restaurant data using a Yelp API, and scraped Michelin restaurant data from Yelp using BeautifulSoup and Splinter.

Reasoning:
- Most robust data tables
- Longest history of data
- Low level of complexity on the Yelp website, allowing us to scrape without a web driver (Jupyter Notebook)

### Data Cleaning
The data was cleaned and merged using Jupyter Notebook. We created two datasets:
1. [Dataset of 179 Michelin star restaurant data with their corresponding Yelp data](Resources/michelin_ML.csv)
2. Dataset of ~7,000 Yelp restaurant reviews, including the Michelin star restaurants from the first dataset

### Data Storage
The datasets were stored in CSV files and SQLite databases.

## Building the Models
We designed

### Machine Learning Models

## What Worked


## What Didn't Work

## Summary
[Google Slides](https://docs.google.com/presentation/d/1rlgLjCL67ObVTJGFYM0-nu0BmKD3xxvakFf2mfFInd4/edit?usp=sharing)
