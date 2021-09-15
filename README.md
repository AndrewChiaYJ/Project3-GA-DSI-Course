# ![](https://ga-dash.s3.amazonaws.com/production/assets/logo-9f88ae6c9c3871690e33280fcf557f33.png) Project 3 - Web APIs and NLP

## Problem Statement
**This project aims to apply machine learning techniques to curate and flag irrelevant content posts within each subreddit so as to improve the quality of users’ experience and grow the active user base for better advertising revenue potential.**

**In classifying the posts, we also want to mitigate the risk of losing users to inappropriate removal of posts when they are actually relevant to the thread.**

## Background

**Situation on Reddit in the year 2020**

1.  52 Million Daily Users
2.  303.4 Million posts
3.  49.2 Billion Upvotes

There are so many users using Reddit, as suggested by the statistics above. One of the reasons is that content optimsation is being emphasised in Reddit, and this is a cornerstone with high impact on user retention, engagement and growth. In the year 2020, there are more than 100 million posts removed in 2020 by moderators.

There are 2 types of moderators in Reddit.

1)  **Human Moderator**

-   There are >70,000 volunteers who volunteer their time to help guide and create Reddit's many communities.
-   They are able to do the followings:
    -   Report or remove comments or submissions containing certain words or phrases.
    -   Ban spammers or other redditors who may be breaking community rules from posting or commenting in their community.

2)  **Auto Moderator**

-   Auto moderator tool is introduced in 2019.
-   It is a system built into reddit that allows moderators to define "rules" to be automatically applied to posts in their subreddit.
-   The Auto Moderator is able to report or remove comments or submissions containing certain words or phrases.


In order to improve moderation efforts and content optimsation to make a more vibrant reddit community, we can:

1) Scope to further curate posts for relevance, as relevant posts keep users reading and engaged.

2) Ease the moderation work by leveraging on machine learning tools to help moderators complete key tasks with less time. We can also do so by having more moderators stepping up to support communities.

## Data Dictionary
Data Dictionary for all datasets are being stored in this link below:
[Data Dictionary](http://localhost:8888/notebooks/OneDrive/Desktop/DSI23%20-%20Project%203/Code/Appendix%20-%20Data%20Dictionary.ipynb)

## Data Used in Analysis
2 subreddit posts contents have being used as datasets for analysis, both being scrapped via **Web APIs**.
1) r/stocks
- The subreddit is created on 27 June 2008, and have 2.9 million community members.
- Data size is 1700, time range is from July 21, 2021 to July 22, 2021.
2) r/CryptoCurrency
- The subreddit is created on 11 March 2013, and have 3.3 million community members.
- Data size is 1700, time range is from July 17, 2021 to July 21, 2021.

## Outline of Workflow
1. Web Scrapping via APIs
2. Data Cleaning/Preprocessing
3. EDA
4. Modelling
5. Recommendations

## Data Cleaning/Preprocessing
Following steps are being done to clean and preprocess the data.
1. Data Cleaning
- Filter away null values and post with [removed]
- Remove duplicate entries
2. Natural Language Processing Techniques
- Removing punctuations
- Tokenizing
- Remove stopwords
- Done lemmatization
3. Vectorization
- Count Vectorization
- N-Gram Vectorization
- TF-IDF Vectorization

## EDA
**1. Length of subreddit posts by Word Count**
- Stocks subreddit have higher mean due to presence of more post >2000 words.
- Based on distribution, most post from both subreddits have < 400 words.

**2. Most related words to "Stocks" & "Crypto"**

By using Word Vectorization, following words are top 10 related words with ‘stocks’ and ‘crypto’:
'stocks': dip, buying, sell, **btc**, buy, selling, **eth**, hold, spacs, back.
'crypto': investing, hey, everyone, curious, trying, someone, guy, hope, wondering, best.

However, words belonging to  Cryptocurrency category (btc, eth) appears in words related to stocks.

Therefore, this highlights the potential challenge we will faced in classification modelling later.

**3. 1-word appear frequently in ‘Stocks’**

*Most words are not a surprise:*
- ‘company’: Stocks is a company’s equity.
- ‘market’: Place that we buy/sell stocks.
- ‘price’: Indicator on how a stock performs.
- ‘share’: Synonym to stock.

*Some Insights*
- There are some words that shows optimism towards the stock market
Words: ‘buy’, ‘growth’, ’good’

**4. 1-word appear frequently in ‘CryptoCurrency’**

*Most words are not a surprise:*
- ‘market’: Place that we buy/sell crypto.
- ‘coin’: Synonym to cryptocurrency.
- ‘price’: Indicator on how a cryptocurrency performs.

*Some Insights*
The most discussed cryptocurrency is Bitcoin
- Words: ‘bitcoin’, ’btc’

**5. 2-words appear frequently in ‘Stocks’**

- price target’: while buying/selling stocks, people set a price target to rip the gain or to stop loss.
- ‘market cap’: total dollar market value of a company’s outstanding shares of stock.

**6. 1-word appear frequently in ‘CryptoCurrency’**

*Some Insights*
1.  Some words indicating the more discussed cryptocurrency
-	“gtpoplt gtpoplt” - Gifto, PlanetPay
- “btc eth” - Bitcoin, Ethereum

2. Mixed sentiments in crypto market due to high volatility
- “bull run” + “bull market” v.s. “bear market” + “buy dip”

## Modelling
### Model Preparation
1) Train/Test Split

2) Vectorization of data done
- Count Vectorizer
-  TF-IDF Vectorizer

3. 2 different classification model is used for modelling
- Multinomial Naive Bayes
- Logistic Regression

### Model Evaluation
|Types of Vectorization Used |Types of Model Used for Prediction |Accuracy Score of Prediction | Recall Score of Prediction|
|:---:|:---:|:---:|:---:|
|**Count Vectorization**|**Multinomial Naive Bayes Model**|0.932|0.873|
|**TFIDF Vectorization**|**Multinomial Naive Bayes Model**|0.962|0.941|
|**Count Vectorization**|**Logistic Regression Model**|0.959|0.967|
|**TFIDF Vectorization**|**Logistic Regression Model**|0.981|0.984|


**Out of the 4 Vectorization Type-Model Type combination, Logistic Regression used on dataframe from TFIDF Vectorization gives the highest accuracy score and recall score. Hence, this particular combination will be used for the model evaluation below.**

 #### The model performance  is strong
Accurate classification > 98% of the time; 1001 out of 1020 predictions
Sensitive classification ~98% relevant post detected
Out of 510 relevant posts, only 19 will be mis-labelled (~3%)

Some keywords are strong predictors of a post’s relevance to r/stocks or r/CryptoCurrency:
- Keywords for r/stocks: Stock, company, share, etf
- Keywords for r/CryptoCurrency: Crypto, coin, bitcoin, btc, eth

## Recommendations

1.  Deploy the model for testing with live data

Given the strong performance of the model (98% accuracy score and 98% sensitivity score), we can benefit from deploying the model for pilot testing on the reddit platform.

2.  Flag posts classified as irrelevant for moderators' assessment

There is a risk of incurring user frustrations if relevant posts are removed as a result of the model misclassification. To minimize wrongful post(s) removal, we can use the model's recommendation to flag posts for moderators' consideration.

3.  Share keywords insights with the moderators

This can help moderators set rules for content posting using the AutoModerator to ensure irrelevant topics will not be posted within the community.

## Future Steps

1. Collect data samples across a longer time (e.g. the past year) for training and model optimisation to pre-empt risk that the topics of discussion and keywords may change across different times of the year


2. Train the data using irrelevant posts from more than one source


3. Train and further optimise the model for production across more subreddit communitiesThis would allow us to evaluate the percentage % of houses that are sold across all neighborhoods.
