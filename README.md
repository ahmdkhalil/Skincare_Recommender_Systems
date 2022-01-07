# Skincare_Recommender_Systems

Selecting a product has always been a hassle for me especially from large suppliers such as Sephora. 

Here is an example on how to select a product and how long it’ll take to choose the one that is suitable. 

[Spehora gif](https://github.com/ahmdkhalil/Skincare_Recommender_Systems/blob/main/images/sephora-app-gif.gif)

Imagine looping through these before ending up with your preferred one.

My goal is to solve that problem. 

Objectives:

1. Build a recommender system for a cold start problem that inputs individual data and outputs recommended products based on the inputs given

Inputs:

1. Recommender Model 1: User Features: Skin type, Skin tone, Eye colour, Hair colour. 
2. Recommender Model 2: Product Features: Ingredients List

What are the different types of Recommender Systems:

1. Collaborative Filtering
2. Content-based Filtering

![EE53AA33-D659-4A03-AC1E-E53B659BFB84.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/451e35f3-be6a-499e-803c-a929401f1ee0/EE53AA33-D659-4A03-AC1E-E53B659BFB84.png)

Here’s an example of a movie recommender system

In this project,

Model 1 is most similar to Collaborative Filtering.

Model 2 is most similar to Content-based Filtering. 

The dataset is forked from this github. 

…….

After cleaning the data the end result of the data are as follow:

(Insert table)

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
