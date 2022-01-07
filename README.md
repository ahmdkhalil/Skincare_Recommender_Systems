# Skincare_Recommender_Systems

## Introduction

Selecting a product has always been a hassle for me especially from large suppliers such as Sephora. Here is an example on how to select a product and how long it’ll take to choose the one that is suitable: 

<p align="center">
<img src="https://github.com/ahmdkhalil/Skincare_Recommender_Systems/blob/main/images/sephora-app-gif.gif" alt="sephora-gif" style="width:200px;"/>
</p>

Imagine looping through these before ending up with your preferred one.

## Objective

1. Build a recommender system for a cold start problem that inputs individual data and outputs recommended products based on the inputs given

Inputs:

      1. Recommender Model 1: User Features: Skin type, Skin tone, Eye colour, Hair colour. 
      2. Recommender Model 2: Product Features: Ingredients List

What are the different types of Recommender Systems:

1. Collaborative Filtering
2. Content-based Filtering

Here’s an example of a movie recommender system:


<p align="center">
<img src="https://github.com/ahmdkhalil/Skincare_Recommender_Systems/blob/main/images/types-of-rec-sys.png" alt="sephora-gif" style="width:800px;"/>
</p>


In this project,

Model 1 is most similar to Collaborative Filtering.

Model 2 is most similar to Content-based Filtering. 

The dataset is forked from this github repo: https://github.com/agorina91/final_project

### Some useful notes from OP:
A note on data acquisition and feature engineering: I scraped Sephora.com using selenium webdriver and got two dataframes: user data and product data. They were merged together on unique user id, cleaned, which resulted in a big dataframe with the following columns: 'Username', 'Skin_Tone', 'Skin_Type', 'Eye_Color', 'Hair_Color','Rating_Stars', 'Review', 'Product', 'Brand', 'Price', 'Rating','Ingredients', 'Combination', 'Dry', 'Normal', 'Oily', 'Sensitive','Category', 'Product_Url', 'User_id', 'Product_id','Ingredients_Cleaned', 'Review_Cleaned', 'Good_Stuff', 'Ing_Tfidf'.

### My Analysis:
Little informaton was given on how OP ended up with the final data but the data clearly shows each user's review for a product and other features related to the user and product. We could see that preprocessing and cleaning were done for the review and ingredient columns. The 'Good_stuff' column suggests that it correlates with the rating stars. Amongst the user features, for some reason only the Skin_Type data column were hot encoded.


After cleaning the data the end result of the data are as follow:

8649 entries, 0 to 8702
Data columns (total 16 columns):
| # | Column |     Non-Null Count | Dtype | 
---  ------        --------------  -----  
| 0   Username      8649 non-null   object 
| 1   Skin_Tone     8649 non-null   object 
| 2   Skin_Type     8649 non-null   object 
| 3   Eye_Color     8649 non-null   object 
| 4   Hair_Color    8649 non-null   object 
| 5   Rating_Stars  8649 non-null   int64  
| 6   Review        8649 non-null   object 
| 7   Product       8649 non-null   object 
| 8   Brand         8649 non-null   object 
| 9   Price         8649 non-null   int64  
| 10  Rating        8649 non-null   float64
| 11  Ingredients   8649 non-null   object 
| 12  Category      8649 non-null   object 
| 13  Product_Url   8649 non-null   object 
| 14  User_id       8649 non-null   int64  
 15  Product_id    8649 non-null   int64 

EDA

User features

Ratings vs Rating Stars

 reviews wordcloud

Num of Products per Category

Ingredients wordcloud each category

Modelling

1. Correlation similarity
2. SVD

Evaluation:

1. SVD 
    1. MSE
    2. RMSE
2. Side by side comparison

Conclusion and Future Works

# Conclusion 

Building a recommender system is not that hard once you get the hang of it. To evaluate whether it works is another thing especially for a cold start problem and a small dataset. 

After a few ticks, I exhausted myself and chose not to move forward with the recommendation based on ingredients preference.


## Summary:

In summary I have built a recommender systems that inputs user features: Skin type, Skin tone, Eye Color, Hair color and outputs the recommmended products for that user.

The first model I ran a simple recommender that returns the highes correlated products based on the features given.
The second model I ran SVD.

Evaluation for SVD is quite bad, scoring:
1. MSE:  1.8
2. RMSE:  1.3

If were to compare results to the first model. Definitely SVD is better choice.


## Future Works:

In the future, I am planning to experiment on different models such as LightFM etc and different evaluation metrics to find the better recommender system.

I would like to continue my project for the ingredients based recommender too.

And to conclued the projects I will definitely try to deploy on a web app in the future.


### Resources:

1. [EDA step by step guide](https://www.analyticsvidhya.com/blog/2021/05/exploratory-data-analysis-eda-a-step-by-step-guide/)
2. [Why are outliers important?](https://towardsdatascience.com/outlier-why-is-it-important-af58adbefecc)
3. [Analyzing Documents with TF-IDF](https://programminghistorian.org/en/lessons/analyzing-documents-with-tfidf)
4. [TF-IDF Code](https://buhrmann.github.io/tfidf-analysis.html)
5. [Plot percentiles](https://towardsdatascience.com/take-your-histograms-to-the-next-level-using-matplotlib-5f093ad7b9d3)
6. [Definition of Percentiles](https://www.thoughtco.com/what-is-a-percentile-3126238)
7. [Simple Matrix Creation](https://towardsdatascience.com/recommender-system-in-python-part-2-content-based-system-693a0e4bb306)
8. Recommender Metrics
    - [Article](https://towardsdatascience.com/evaluation-metrics-for-recommender-systems-df56c6611093)
    - [Code example](https://github.com/statisticianinstilettos/recmetrics/blob/master/example.ipynb)
9. [Mean of Average Precision (MAP)](http://sdsawtelle.github.io/blog/output/mean-average-precision-MAP-for-recommender-systems.html)
