
# Project 3 - NLP and API
#### By: Joshua Burns

### Problem Statement  

Reddit is a news and social aggregating site where users can post content into categorical pages, called subreddits. Reddit has countless subreddits based on users interests and needs, many of which are very helpful to understand a variety of topics. Users are able to post, comment, and vote on the submissions gaining an aggregated score on that post.  

Since the dawn of the 2 party system, Liberals and Conservaties have been at the center of the political scene. As we've seen in recent years, the ideals of both sides couldn't be more diametrically opposed. As such, if we pull the data from posts from the respective subreddits, we should be able to easily classify which post belongs to which subreddit.  

With this project, we look to compare two different subreddits aggregated posts side by side to check for similarities and differences. Using natural language processing, can we use machine learning to correctly classify which subreddit a post belongs to?

### Executive Summary
To begin, data was pulled from from two different subreddits. In order to simplify the process, the Pushift Reddit API was used. The Pushift API can pull 100 posts at a time from the desired subreddit based on title or comment as directed by the user and is returned in the JSON format, ready to be converted into a dataframe for functional usage. In our case, the subreddits sourced were r/Liberal and r/Conservtive, potentially giving us enough polarity to distinguish a post from another, as well as a topical umbrella to work under.  

Once imported and converted, I looked through the categories to see what may be relevant to my task of predicting classifications. Out of the over 75 categoried collected by the Pushift API, I kept 9 columns for my evaluation after checking for completeness, most notably: subreddit (converted to sub), title, user, and domain. data cleaning for this project was fairly straightforward, as we knew from the start what our target variable and predictors were going to be. A quick search for null values returned very few and I was able to proceed to Exploratory Data Analysis.  

Through the EDA process, I looked to identify trends in the data that may point in the right direction for how to proceed in classifying the posts. The process for all of the EDA was very similar: implement a count vectorizer and check for term frequency, both in individual dataframes and also in a larger concatenated dataframe. I looked at several sets of words to identify similarities and differences, as well as checking for unique users and whether or not they posted in one or both subreddits and how frequently.  

Now the data was ready for modeling. Pipelines were implemented to streamline the process of transforming the title column into a useable form for classification models, as well as converting the target variable, subreddit, into binary values for modeling. Train, test, split with stratification was performed on both variables and a baseline accuracy of 50% was confirmed.  

Finally, the models were fit. Ultimately, I implemented 3 different model types, Logistic Regression, Bernoulli Naive Bayes, and Random Forests. Bernoulli Naive Bayes was implemented in conjunction with a count vectorier and TFIDF in separate models, bringing our total number of independent models to 4. A confusion matrix was creadted for each of the models, with the more complex models showing a pre and post-parameter tuning. My target metric was accuracy score and all final results are listed below.  

### Conclusions and Recommendations  

|Model|Training Accuracy<br/>Score|TestingAccuracy<br/>Score|Correctly<br/>Classified|Incorrectly<br/>Classified|
|---|---|---|---|---|
|Logistic<br/>Regression|0.887|0.724|1,195 posts|455 posts|
|<br/>Bernoulli NB/<br/>Count Vectorizer<br/>|0.834|0.712|1,174 posts|476 posts|
|<br/>Bernoulli NB/<br/>TFIDF<br/>|0.881|0.725|1,197 posts|453 posts|
|<br/>Random Forest<br/>|0.998|0.702|1,159 posts|491 posts|

As shown in the table above, all of the classification models exceeded the baseline accuracy expectation. All performed reasonable well with the data given, however there still stands to be quite some improvement to be found in future modeling. Logistic Regression and Bernoulli Naive Bayes performed almost identically, Logistic Regression with zero parameter tuning and Bernoulli NB tuned to the best of my ability.  

Unfortunately, against predictions, all of the models performed fairly poorly when presented with new data to predict, finishing across the board with accuracy scores below 75%.  
