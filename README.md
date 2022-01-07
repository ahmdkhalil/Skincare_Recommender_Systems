# Skincare_Recommender_Systems

## Introduction

Selecting a product has always been a hassle for me especially from large suppliers such as Sephora. Here is an example on how to select a product and how long it’ll take to choose the one that is suitable: 

<p align="center">
<img src="https://github.com/ahmdkhalil/Skincare_Recommender_Systems/blob/main/images/sephora-app-gif.gif" alt="sephora-gif" style="width:300px;"/>
</p>

Imagine doing this repetitively until you found your preferred product. 

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

---------------------------------------------------------------------
# Content:
## 1. Data Collection
## 2. Data Cleaning
## 3. EDA
## 4. Modelling & Evaluation
## 5. Conclusion & Future Works

---------------------------------------------------------------------

# Data Collection

The dataset is forked from this github repo: https://github.com/agorina91/final_project

### Some useful notes from OP:
A note on data acquisition and feature engineering: I scraped Sephora.com using selenium webdriver and got two dataframes: user data and product data. They were merged together on unique user id, cleaned, which resulted in a big dataframe with the following columns: 'Username', 'Skin_Tone', 'Skin_Type', 'Eye_Color', 'Hair_Color','Rating_Stars', 'Review', 'Product', 'Brand', 'Price', 'Rating','Ingredients', 'Combination', 'Dry', 'Normal', 'Oily', 'Sensitive','Category', 'Product_Url', 'User_id', 'Product_id','Ingredients_Cleaned', 'Review_Cleaned', 'Good_Stuff', 'Ing_Tfidf'.

### My Analysis:
Little informaton was given on how OP ended up with the final data but the data clearly shows each user's review for a product and other features related to the user and product. We could see that preprocessing and cleaning were done for the review and ingredient columns. The 'Good_stuff' column suggests that it correlates with the rating stars. Amongst the user features, for some reason only the Skin_Type data column were hot encoded.

------------------------------------------------------------------

# Data Cleaning

## Missing values

Values with no data are in top 1 or 2. The numbers are similar.

- Skin Tone 'No data' = 2102
- Skin Type 'No data' = 2106
- Eye Color 'No data' = 2085
- Hair Color 'No data' = 2092

Ingredient columns list shows more interesting data: aside from 'no info' in the top frequency, there are two other values that are not ingredient, 'Visit the Shiseido boutique' & 'Visit the SEPHORA COLLECTION boutique'.

### Removed/Dropped
1. No data values from user features.
2. No info values from ingredients column.
3. 'Visit the Shiseido boutique' & 'Visit the SEPHORA COLLECTION boutique' from ingredients column.



#### After cleaning the data the end result of the data are as follows

Original = 8649 entries. Final = 6260 entries


| #  | Column       | Dtype  | Description |
| -- | ------------ | ------ | ----------- |
| 0  | Username     | string | Username of the product reviewer |
| 1  | Skin_Tone    | string | User skin tone from 9 different tones: Light, Fair, Medium, Olive, Tan, Procelain, Deep, Dark, Ebony |
| 2  | Skin_Type    | string | User skin type from 4 different types: Combination, Oily, Dry, Normal |
| 3  | Eye_Color    | string | User eye colour: Brown, Blue, Hazel, Green, Grey|
| 4  | Hair_Color   | string | User hair colour: Brunette, Blonde, Black, Auburn, Red, Gray|
| 5  | Rating_Stars | integer| User rating stars of the product |
| 6  | Review       | string | User review of the product |
| 7  | Product      | string | Product name | 
| 8  | Brand        | string | Product brand |
| 9  | Price        | integer| (USD) |
| 10 | Rating       | float  | Average rating of the product from the collected users |
| 11 | Ingredients  | string | Ingredients of the product |
| 12 | Category     | string | Product category|
| 13 | Product_Url  | string | Product url website|
| 14 | User_id      | integer| User id|
| 15 | Product_id   | integer| Product id|

### Outliers
I will not remove any outliers from this data. Although it is understood that during production might slip a tiny percentage resulting in bad ratings and reviews. In that case the fair approach is removing outliers from each and every product one by one. This will take too much time to iterate through 300 unique products as you can see from the code below.


<code>print(df_drop1['Product'].nunique()) </code>
       
300 

For this project I will choose to ignore the outliers. Outliers will be included in the modelling.

---------------------------------------------------

# EDA

I performed EDA to understand the data better such as the User Features:

<p align="center">
<img src="https://github.com/ahmdkhalil/Skincare_Recommender_Systems/blob/main/images/features-after.png" style="width:800px;"/>
</p>

### Define the metrics for the model
- For User to User Filtering use the Rating Stars as the metric.
- For Product Ingredient use the Rating column as the metric.

### Rating vs Rating Stars column distribution
<p align="center">
<img src="https://github.com/ahmdkhalil/Skincare_Recommender_Systems/blob/main/images/ratingvsratingstars.png" style="width:800px;"/>
</p>

### Rating Percentile

<p align="center">
<img src="https://github.com/ahmdkhalil/Skincare_Recommender_Systems/blob/main/images/percentile-rating.png" style="width:800px;"/>
</p>

### Number of Products per Category

<p align="center">
<img src="https://github.com/ahmdkhalil/Skincare_Recommender_Systems/blob/main/images/num-prod-each-cat.png" style="width:800px;"/>
</p>

## Preprocessing text data

### Preprocessing

#### Review column:
    1. Tokenize
    2. Lemmatize
    3. Remove stopwords, punctuation etc
    4. TF-IDF
    
#### Ingredients column:
    1. Tokenize
    2. Lemmatize
    3. Remove stopwords, punctuation etc
    4. WordCloud
    
### Ingredients WordCloud of each Category

<p align="center">
<h4 style="font-size:30px;">Cleanser</h4>
<img src="https://github.com/ahmdkhalil/Skincare_Recommender_Systems/blob/main/images/wordcloud-cleanser.png" title="Cleanser" style="width:400px;"/>
</p>

<p align="center">
<h4 style="font-size:30px;">Facemask</h4>
<img src="https://github.com/ahmdkhalil/Skincare_Recommender_Systems/blob/main/images/wordcloud-facemask.png" title="Facemask" style="width:400px;"/>
</p>

<p align="center">
<h4 style="font-size:30px;">Mositurizer</h4>
<img src="https://github.com/ahmdkhalil/Skincare_Recommender_Systems/blob/main/images/wordcloud-moisturizer.png" title="Moisturizer" style="width:400px;"/>
</p>

<p align="center">
<h4 style="font-size:30px;">Treatment</h4>
<img src="https://github.com/ahmdkhalil/Skincare_Recommender_Systems/blob/main/images/wordcloud-treatmetn.png" title="Treatment" style="width:400px;"/>     
</p>

--------------------------------------------------

# Modelling and Evaluation

High user feature count in descending order:

<p align="center">
<img src="https://github.com/ahmdkhalil/Skincare_Recommender_Systems/blob/main/images/user-features-combined.png" style="width:900px;"/>     
</p>


## Modelling

1. Correlation similarity
2. SVD

Before modelling I ran a long-tail plot to remove any popular product.

<p align="center">
<img src="https://github.com/ahmdkhalil/Skincare_Recommender_Systems/blob/main/images/long-tail-plot.png" style="width:900px;"/>     
</p>


Usually only a small percentage of items have a high volume of interactions, and this is referred to as the “head”. Most items are in the “long tail”, but they only make up a small percentage of interactions but in the sephora products case most of its items has high ratings from users.

This makes it easy for a recommender system to learn to accurately predict these items. The objective of this recommendation is mainly focus on cold start problems where the user don't have any history purchase and wants to product reommendation on their inputs (user features and ingredients)

### Results for the models:

<p align="center">
<h3 style="font-size:30px;">Inputs: Dry, Light, Hazel, Blonde</h3>
<img src="https://github.com/ahmdkhalil/Skincare_Recommender_Systems/blob/main/images/corr_sim-dry-light-hazel-blonde.png" width="700" height="300";"/>     
</p>

<p align="center">
<h3 style="font-size:30px;">SVD Prediction Result</h3>
<img src="https://github.com/ahmdkhalil/Skincare_Recommender_Systems/blob/main/images/svd-pred.png" width="800" height="200";"/>     
</p>


## Evaluation:

1. SVD 
    1. MSE: 1.8
    2. RMSE: 1.3
2. Side by side comparison, inputs user features: Combination, Dark, Brown, Black

<p align="center">
<img src="https://github.com/ahmdkhalil/Skincare_Recommender_Systems/blob/main/images/corr_sim-comb-dark-brown-black.png" width="700" height="300";"/>  
</p>
                                                                                                                                                   
<p align="center">                                                                                                                                                   
<img src="https://github.com/ahmdkhalil/Skincare_Recommender_Systems/blob/main/images/svd-pred2.png" width="800" height="200";"/> 
</p>

--------------------------------------------------------

# Conclusion and Future Works

Building a recommender system is not that hard once you get the hang of it. To evaluate whether it works is another thing especially for a cold start problem and a small dataset. 

After a few ticks, I exhausted myself and chose not to move forward with the recommendation based on ingredients preference.


## Summary:

In summary I have built a recommender systems that inputs user features: Skin type, Skin tone, Eye Color, Hair color and outputs the recommmended products for that user.

The first model I ran a simple recommender that returns the highes correlated products based on the features given.
The second model I ran SVD.

Evaluation for SVD is quite bad, scoring:
1. MSE:  1.8
2. RMSE:  1.3

If were to compare results to the first model. Definitely SVD is a better choice.


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
