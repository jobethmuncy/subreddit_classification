<h1>Subreddit Classificatoin: Web APIs & NLP</h1>

<h3>Problem Statement</h3>

<p>"What are you having to drink? Many people will either have an answer right off the bat or mull it over for awhile and then say, “I’m not sure. Do I want a cocktail or wine? Do I want to start with a cocktail and then get wine?” In this project, two subreddits were examined. Subreddit wine has has 113K members and subreddit cocktails has 171K member. Data from these two subreddits will be processed classification models applied to this data. Can the model correctly classify a subreddit comment as ‘wine’ or ‘cocktail’?</p>

<h3>Executive Summary</h3>

<p>Data was gathered from Reddit's Pushshift API with 2 different endpoints:<br> 
Submission (https://api.pushshift.io/reddit/search/submission)<br>Comment (https://api.pushshift.io/reddit/search/comment)<br><br> First data was examined from the submission API. The categories of ‘subreddit’, ‘title’, and ‘selftext’ were used. Many people submit photos as their selftext and brief titles. There was not enough data to work with from this endpoint so the comments were used instead. 50,000 comments were taken from each subreddit category to be used in the model. The categories used were ‘subreddit’ and ‘body’. </p>
<p>Before using the model to classify these comments, the data was cleaned. First the HTML artifacts were removed. Next, all non-letters were removed using regex. This took away all numbers, punctuation, and emojis from the text data. The text was then put into all lowercase and the strings of text were split into individual tokens. English stopwords were removed and the words were lemmatized. This clean text data was mapped onto the data frame. </p>
<p>Looking at the top ten most common words in each subreddit, ‘like’ and ‘one’ both appeared in both lists. These were removed with the stopwords as well.  After the data was cleaned, 309 cocktail comments and 357 wine comments were missing. This meant that the text that was there had been filtered out in one or all steps listed above. As there were 100,000 comments initially brought it, these 666 empty lines were dropped from the data.</p>
|---|Initial Word Count|Clean Word Count|Unique Words|% Words Removed|% Unique Words to Original|% Unique Words to Clean|
|---|---|---|---|---|---|---|
|<strong>Cocktail</strong>|1,460,871|818,864|40065|43.9%|2.7%|4.8%|
|<strong>Wine</strong>|1,718,265|906,371|51,140|47.2%|2.9%|5.6%|<br>
<p>Baseline models were made for the data. Both CountVecotrizer and TfidfVectorizer were used to turn the text data into numerical data for the different classifiers. For the baseline models, MultinomialNB and LogisticRegression were used as the classifiers. Later, SVC and LinearSVC were also tested with CountVectorizer. There was high overfitting in those two models and a loss in accuracy so these were not pursed further <br><br>
Scores listed as <strong>Train : Test</strong></p>
|---|MultinomialNB|LogisticRegression|SVC|LinearSVC|
|---|---|---|---|---|
|CountVectorizer|88.84%  :  86.94%|91.83%  :  86.53%|90.07%  :  84.98%|93.74%  :  85.94%|
|TfidfVectorizer|85.52%  :  86.94%|90.37%  :  86.82%|---|---|
