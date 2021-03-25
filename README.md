# Song Recommendation System
Song Playlist Recommender System Using Machine Learning Techniques With Spotify Dataset

This project attempt to develop a recommender system for automating playlist generation by the addition of relevant songs, hence extending a current playlist beyond the last song. Our focus is on enhancing user experience when listeners are in an ‘open’ mindset (40% of the time), as stated above.


### Dataset
Dataset Used : https://github.com/vaslnk/Spotify-Song-Recommendation-ML/tree/master/data 

About the Dataset: 
The dataset is from Spotify Million Playlists (Recsys 2018) Challenge [2]. The dataset contains a million user-generated playlists. These playlists were created during the period of January 2010 through October 2017. Each playlist in the MPD contains a playlist title, the track list (including track metadata) editing information (last edit time, number of playlist edits) and other miscellaneous information about the playlist.


### Overview

Collaborative approaches will require reinterpretation of user-item collaborative filtering approach. In traditional 
perspective of user-item collaborative filtering, the model will look at users who have similar behaviours to another particular user based on similar ratings and recommend items/product those similar users also liked. Essentially, “Users who are similar to you, also liked ….” approach. 

For this problem, I will treat “user” as “playlist” and “item” as “track”(i.e. song). This approach was taken based on data provided from the selected dataset. I will also reinforced the selected dataset with further data extracted from Spotify API.   

The assumption of this approach for collaborative filtering model is based on idea that we should select songs from playlists which are similar to the starting playlist. The second part of the assumption is that similar songs from playlists which are similar to starting playlists are more similar to songs in starting playlists.    

### 3 Approaches To Solving The Collaborative Filtering

1)	Using Cosine Similarity 
2)	Using Matrix Factorization Method
3)	Using Stacking Classifier Ensemble Method 

Each of these approaches broadly follows the macro idea of two step process: First step is finding similar playlist to ‘query playlist’ (which is the playlist which is the subject here). Second step is finding songs which are similar to those in query playlist and determine a performance score. 

Key terminology: ‘Query playlist’ refers to the playlist which we intend to find songs to add on to. 

Key Underlying Condition: In real use case, a user’s playlist represent a subset of the “ground truth” playlist (called “query playlist’ in this project- which  contains the complete number of songs). So the following segment of this project is to examine the various models’ effectiveness in identifying the “right” songs to recommend. The “right” songs being those which are not in user’s playlists but are in “query playlist” (which is the ground truth).  The models’ ability to perform this role is examined here.  

### 3) Using Stacking Classifier Ensemble Method

Ensemble learning improves machine learning results by combining several models into one predictive model in order to decrease variance, bias and improve prediction.

The approach starts off by using Jaccard Similarity to get the closest match between two playlists. Jaccard coefficient measures similarity between finite sets. In order to obtain finite sets of information for each playlist, we have to transform ‘pos’(which represent position in playlist)  in existing dataset to ‘1’ or ‘0’. ‘1’ if song is in playlist.’0’ if song is not in playlist . Next a Jaccard Similarity matrix is generated. From this matrix, extract the most similar playlist’s song set.

The next step to get the best song, will involve the use of Stacking Classifier Ensemble. This second step will attempt to get build a model that can best identify songs in the most similar playlist to recommend, based on audio features for the song. The work here requires the acceptance of “Key Underlying Condition” mentioned in the beginning of this section.  

The following five algorithms are used in stacking ensemble: 1) Logistic Regression, 2) K-Nearest Neighbors, 3) Decision Tree, 4)SVC and 5) Gaussian Naïve Bayes. They are selected because they are all classifiers and represent diverse algorithms. In addition, two meta learners are compared. Namely, Logistic Regression and Gradient Boosting Classifier. Gradient Boosting is selected as it seems to give better result. GridSeachCV is used to find predefined hyperparameters to get the best hyperparameters for each base model. Getting better tuned base models improves prediction for the Stacking Classifier Ensemble. 

