# GA DSI Capstone Project: 
## NLP Predictions of Jeopardy Clues
Author: Joshua Burns
github: [https://github.com/jburns10/jburns10](https://github.com/jburns10/jburns10)

## Contents:
Welcome!  
This repo contains a collection of work for my Capstone Project for the Data Science Immersive program at General Assembly. Within this repo, you will have access to all Jupyter notebooks used for the process, csv files of all data, my in-class presentation slides and the visual aides used within.  

## Necessary Packages / Libraries:
- textstat
- re
- all other packages should be available with Anaconda base install

## Links to Work:
1. [EDA & Preprocessing Notebook](https://git.generalassemb.ly/jburns10/dsir-125/blob/master/assignments/projects/capstone/01-eda-preprocessing.ipynb)
2. [Clustering Notebook](https://git.generalassemb.ly/jburns10/dsir-125/blob/master/assignments/projects/capstone/02-clustering.ipynb)
3. [Modeling Notebook](https://git.generalassemb.ly/jburns10/dsir-125/blob/master/assignments/projects/capstone/03-modeling.ipynb)
4. [Datasets Used & Produced](https://git.generalassemb.ly/jburns10/dsir-125/tree/master/assignments/projects/capstone/datasets)
5. [In-Class Presentation Slides](https://git.generalassemb.ly/jburns10/dsir-125/tree/master/assignments/projects/capstone/presentation)

## Executive Summary
Jeopardy! America's favorite quiz show.  
<br/>
Jeopardy, a daily episodic quiz show, has been around since 1984. It pits 3 contestants against each other to respond in the form of a question to a given clue. For those who may not know, Jeopardy consists of 2 rounds of 30 answers (which are actually the questions) that contestants need to be respond to in the form of a question (the answer in layman's terms). Both rounds consist of 6 categories, with 5 questions per category, increasing in dollar value incrementally as the contestants work their way down the game board. In the early years of Jeopardy, the values of first round questions ranged from \\$100 to \\$500, while the second round ranged from \\$600 to \\$1000, increasing by \\$100 with every question. In 2001, Jeopardy doubled the values of all of the questions, and it remains the same to this day. Each round also contains randomly placed "Daily Doubles," one in the first round and two in the second, where a contestant can wager up to and including their total earnings to that point or the maximum value of the top clue in that round, whichever is the greater value.  
<br/>
The contestants' goal is to accrue as much money as they can before the end of the second round, when they will once again wager any of their total earnings based on the category of the final clue. The winner of the final round is the contestant who retains or earns the highest dollar amount, whether or not the contestant got the final response correct. The winner keeps their earnings and is allowed to return as a champion for the next episode.  
<br/>
This project seeks to assemble the top categories used by Jeopardy over the years and use natural language processing to determine which category a given clue falls into.  
<br/>
Source: Game information mostly from personal knowledge; dates of changes pulled from [Jeopardy Wikipedia](https://en.wikipedia.org/wiki/Jeopardy!#First_two_rounds)

## Data
Data for this project was sourced from  [Kaggle](https://www.kaggle.com/prondeau/350000-jeopardy-questions?select=master_season1-35.tsv) and came in .tsv format. The original data was sourced on [reddit.com](https://www.reddit.com/r/datasets/comments/cj3ipd/jeopardy_dataset_with_349000_clues/) by user [prondeau](https://www.kaggle.com/prondeau). 
<br/>
The data contains 36 years of Jeopardy questions and answers dating from the inaugural season in 1984 through 2019. The file was cleaned at the source to remove any "impossible" video or audio clues, presumably those with no text prompt to accompany the multimedia content, then organized in chronological order.

## Data Dictionary
|Feature Column|Description|
|--------------|-----------|
|round|Round of the show in which the clue appeared.<br/>1:Jeopardy Round, 2:Double Jeopardy Round, 3:Final Jeopardy|
|value|dollar value of a correct answer|
|daily_double|whether the clue was a daily double|
|category|category name on the game board|
|comments|comments from the host about the category|
|answer|the clue prompt shown to contestants|
|question|the correct response to the clue prompt|
|air_date|date the show aired on television|
|notes|special notes about the episode airing|

## Process
#### 1. Data Cleaning
The dataset that was found was very clean and organized upon so initial data cleaning and processing was almost nonexistent. 

#### 2. EDA
Some basic EDA steps were taken first, including checking the shape of the data and checking the data types of all columns. Features were created to further explore the data. Word count and character counts were added to see potentially how detailed the clues tended to be. The word counts were also in an attempt to identify the complexity of the observations from a superficial standpoint. In order to further explore the complexity of the data, the textstat library was implemented which offers several deeper counts, such as lexicon, syllable and sentence counts. Additionally, the textstat library offers several readability scores to evaluate the complexity of a document. For this project, the Dale-Chall readability score was assessed. This score rates a document on approximately 3,000 words, and the more words in the document that fall outside of the vocabulary set, the more complicated the document is deemed, and the higher the score it receives.

#### 3. Model Selection
The data was reduced to include only the top 25 appearing categories in the dataset in the essence of keeping training time down, especially with over 47,000 categories in the original file.  
<br/>
A default parameter Multinomial Naive Bayes model was fit on both a Count Vectorized and a TFIDF Vectorized set of each document in the corpus. Multinomial Naive Bayes was chosen because although it wasn't necessarily meant for text classification, it performs incredibly well to classify the documents.  
<br/>
Once a baseline was established, additional models were fit to try to begin optimization. Overall the desired metric was accuracy throughout the modeling process and all of the default parameter models performed fairly well. Those models fit were: Decision Trees, Random Forests, AdaBoost, Gradient Boost and K-Nearest Neighbors. On the other hand, almost all of the models failed to capture much signal during testing, with all of them returning a below 50% average accuracy rate classifying on testing data.  
<br/>
#### 4. Model Optimization
Optimization began and ended with gridsearching parameters withing the Gradient Boosting Classifier, since it returned the best training and testing accuracy without being completely overfit. During gridsearching, both default parameters and tuned parameters were searched over, in both iterations of the gridsearch. Through these methods, the accuracy was able to crawl closer to 50%, but still ultimately falling short.  
<br/>
#### 5. Conclusion and Recommendations
The Gradient Boosting Classifier struggled to correctly classify several categories, and upon closer inspection, the culprit seems to be that the category types were too similar. Category names such as U.S. History and American History were often split in which one the classifier chose, which makes sense given the. similarities. In this model, after the results were realized, some clustering was attempted to try to capture more signal in the clues, but the clustering process, both KNN and DBSCAN only served to create noise. Moving forward, we could attempt clustering on the target category names to see if the clusters mimic the similarities observed.  
<br/>
Ultimately, further optimization is needed to enhance the performance of this model and to attempt to correctly classify more clues correctly. I am looking forward to pushing the model and metrics further to ensure the model performs at top potential. 