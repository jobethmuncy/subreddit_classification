<h1>Subreddit Classificatoin: Web APIs & NLP</h1>

<h3>Problem Statement</h3>

<p>"What are you having to drink? Many people will either have an answer right off the bat or mull it over for awhile and then say, “I’m not sure. Do I want a cocktail or wine? Do I want to start with a cocktail and then get wine?” In this project, two subreddits were examined. Subreddit wine has has 113K members and subreddit cocktails has 171K member. Data from these two subreddits will be processed classification models applied to this data. Can the model correctly classify a subreddit comment as ‘wine’ or ‘cocktail’?</p>

<h3>Executive Summary</h3>

<p>Data was gathered from Reddit's Pushshift API with 2 different endpoints:<br> 
Submission (https://api.pushshift.io/reddit/search/submission)<br>Comment (https://api.pushshift.io/reddit/search/comment)<br><br> First data was examined from the submission API. The categories of ‘subreddit’, ‘title’, and ‘selftext’ were used. Many people submit photos as their selftext and brief titles. There was not enough data to work with from this endpoint so the comments were used instead. 50,000 comments were taken from each subreddit category to be used in the model. The categories used were ‘subreddit’ and ‘body’.<br>
Before using the model to classify these comments, the data was cleaned. First the HTML artifacts were removed. Next, all non-letters were removed using regex. This took away all numbers, punctuation, and emojis from the text data. The text was then put into all lowercase and the strings of text were split into individual tokens. English stopwords were removed and the words were lemmatized. This clean text data was mapped onto the data frame.<br>
Looking at the top ten most common words in each subreddit, ‘like’ and ‘one’ both appeared in both lists. These were removed with the stopwords as well.  After the data was cleaned, 309 cocktail comments and 357 wine comments were missing. This meant that the text that was there had been filtered out in one or all steps listed above. As there were 100,000 comments initially brought it, these 666 empty lines were dropped from the data.<br>
Baseline models were made for the data. Both CountVecotrizer and TfidfVectorizer were used to turn the text data into numerical data for the different classifiers. For the baseline models, MultinomialNB and LogisticRegression were used as the classifiers. Later, SVC and LinearSVC were also tested with CountVectorizer. There was high overfitting in those two models and a loss in accuracy so these were not pursed further.<br>
The CountVectorizer and MultinomialNB was selected as the best choice to move forward with. All of the models had a test accuracy score between 85%-87% but the selected model only had a 1.9% difference in accuracy from the training data to the testing data score. There is the least amount of bias and variance in this model. From here, GridSearch was used to find the best hyperparameters.<br>
After fitting 240 models on the CountVectorizer and MultinomialNB model, the training score was 95.41% and the test score was 87.58%. There was an increase in accuracy but also in increase in variance. </p>

<h3>Project Directory </h3>
<h4>project_3_master</h4>
    <ul><strong>code</strong>
        <li>01_Get_Data_Cocktail_Subreddit.ipynb</li>
        <li>02_Get_Data_Wine_Subreddit.ipynb</li>
        <li>03_Clean_Cocktails.ipynb</li>
        <li>04_Clean_Wine.ipynb</li>
        <li>05_EDA_and_Modeling.ipynb</li>
    </ul>
    <ul><strong>data</strong>
        <li>clean_50cocktail.csv</li>
        <li>clean_50wine.csv</li>
        <li>cocktails_50comments.csv</li>
        <li>wine_50comments.csv</li>
        <li>friends_test.txt</li>
    </ul>
        <ul><strong>images</strong>
        <li>Top 10 cocktail.png</li>
        <li>Top 10 wine.png</li>
    </ul>
    project_3_reddit_presentation.pdf<br>
    README.md
    
    <h3>Conclusions</h3>
    <p>In conclusion, the model can accurately classify a comment into the categories ‘wine’ or ‘cocktails’ 87% of the time. After trying 452 model combinations with varying hyperparamenters, The CountVectorizer and MultinomialNB model was the best classifier combination. <br>As a short experiment, 15 comments of text about wine or cocktails were gathered from three friends. These comments were cleaned and then ran through this model. It predicted the correct categories with 93% accuracy. This is likely higher than the models accuracy score due to the sampling that was conducted. All three contributors are food and beverage professionals and likely use words that are specific to each category as part of their daily vocabulary. A larger and more diverse sample would like show an accuracy score closer to the model. </p>

<h3>Recommendations</h3>
<p>For further recommendations on this model, related subreddit categories could be added to the current categories. For example, adding ‘winemakers’ to ‘wine’ and adding something like ‘drinking problems’ to ‘cocktails’. This will add an increased vocabulary to the models to fit to and perhaps a higher accuracy score.  </p>
