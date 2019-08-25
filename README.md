# Movie Recommendation Engine by Spark & Elasticsearch

## Introduction
This repo is built for developing large-scale recommender system.

It illustrates how to use Apache Spark for training a collaborative filtering recommendation model from ratings data stored in Elasticsearch, savine the model factors to Elasticsearch, and then using Elasticsearch to serve real-time recommendations community.

The dataset comes from MovieLens which consists of a set of ratings given by users of the MovieLens movie rating sytem to various movies. It also contains meatdata(title and generes) for each movie.

This movie recommender can realize two functions:
* Provide similar movies for a given movie
* Provide movies to a given user


## Preparation
Before excecuting the code, you need setup these(See detail in Jupyter Notebook):
* *Elasticsearch*
* *Elasticsearch vector-scoring plugin*  
The aim of this plugin is to enable real-time scoring of vector-based models, in particular factor-based recommendation models.
* *Elasticsearch Spark Connector*  
It is used to ingest and index user event data into Elasticsearch.
* *Apache Spark*
* *Download Dataset*  
The "small" version of the latest MovieLens movie rating dataset, containing about 100,000 ratings, 9,000 movies and 700 users.

## Steps

**1. Load the movie dataset into Spark.**  
We will be using the following files in the folder ./data/ml-latest-small:\
ratings.csv - movie rating data - (userId, movieId, timestamp, rating given by the user to the movie)\
movies.csv - movie title and genres - (movieId, title, genres)\
links.csv - external database ids for each movie  
**2. Use Spark DataFrame operations to clean up the dataset and load it into Elasticsearch.**  
Create an Elasticsearch index with mappings for users, movies and rating events. Load Ratings and Movies DataFrames into Elasticsearch via Elasticsearch Spark Connector.

**3. Using Spark MLlib, train a collaborative filtering recommendation model.**  
Spark MLlib achieves collaborative filtering using ALS(Alternative Least Squares) which has good performance on sparse matrix and distributed environment.

**4. Save the resulting model into Elasticsearch.**  
The resulting model is movie-factor vectors and user-factor vectors.

**5. Implement Real-time Recommendation by displaying posters of the movies.**  
Using Elasticsearch queries and a custom vector scoring plugin, generate some example recommendations. The [Movie Database API](https://www.themoviedb.org/) is used to display movie poster images for the recommended movies.

compute personalized user and similar item recommendations and combine recommendations with search and content filtering
