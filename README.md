# DSI Project 3: Reddit NLP Classifier
By: Yeo Jia Chi

## Problem Statement:
In finance, the act of investing is to allocate money in the expectation of receiving some benefit in the future. For any good investor, it is expected that their initial investment will do well and return a handsome profit. The challenge however for most aspiring traders is choosing the right stock, and finding the best time to execute their orders.

While online investment forums (such as Reddit) have been very useful in assessing the "market sentiment" of different stocks types, investment opinions which are posted on these subchannels can vary widely based on their user profile and risk appetite. Blindly taking such financial advice without consideration of the background origins can therefore be very dangerous financially.

On Reddit, there are two popular subreddits that users can post their stock analysis and stock purchase decisions. These are:

- r/wallstreetbets
- r/investing

As their names imply, users on the r/wallstreetbets subreddit are of the high-risk/high-reward (almost reckless) category, whereas those on the r/investing channel tend to favour safer forms of investment portfolios.

For the purposes of this project, I will be building a NLP classifier that will help us to distinguish the message posts between these two popular subreddits. By using the Reddit API, posts on these two subreddits will be scraped, processed and used to build our NLP classifier. This classifier will enable us savvy investors to now make informed investment decisions based on our desired investment objectives and risk appetites.

## Executive Summary:
Contents:
1. Problem Statement
2. Executive Summary
3. Importing the Libraries
4. Data Collection using APIs
5. Data Cleaning and EDA
6. Data Preprocessing
7. Data Modelling
8. Analysis of Classification Results
9. Conclusion and Recommendations

## Data Dictionary
For Pushshift.io API, the data dictionary is as follows:

|Feature|Datatype|Description|
|:-------|--------|-----------|
|**author**|object|author of this post|
|**created_utc**|int64|timestamp when the post was created|
|**full_link**|object|link to the post|
|**selftext**|object|post message body|
|**subreddit**|object|post subreddit location|
|**title**|object|post title|

For Reddit API, the data dictionary can be found at the following link:

https://github.com/reddit-archive/reddit/wiki/JSON

## Model Evaluation
|Model|Train_accuracy|Test_accuracy
|:-----|--------------|-------------|
|CVEC/LogReg(default)|0.882|0.849|
|TVEC/LogReg(default)|0.877|0.861|
|CVEC/LogReg(GridCV)|0.912|0.858|
|TVEC/LogReg(GridCV)|0.893|0.868|
|CVEC/MultiNB(GridCV)|0.838|0.828|
|TVEC/GaussNB(GridCV)|0.860|0.828|

The best model is the combination of TVEC with Logistic Regression

## Key Findings
- We have successfully developed a NLP classifier based on CountVectorization and LogisticRegression that is able to accurately classify posts into their respective r/wallstreetbets or r/investing subreddits.
- Enrichments of key words (or slang) between the two subreddits enables the model to function robustly during training and testing.
- NLP allows for additional insights into the subreddit's demographic profile and habits, which is useful for targeted marking strategies.
- Stock trading preferences based on the subreddit's frequently occuring stock tickers can also reveal insights into their trading strategy/plans.
- Our NLP model fails to distinguish the context of messages, hence leading to wrong classification. The model also fails when it appears too "general" in nature, leading to an improper classification.

## Recommendations
As with all models, further improvements and refinements have to be continuously made before and during production. There are three areas which future efforts can be directed towards:

**1) Reduction of noise words**:
- Additional words arising from word artifacts (e.g. Internet links, html-coding, file.types) can be removed during vectorization.
- Words that appear too "general" in nature can also be considered for removal (e.g. "stock"), but a better approach would be to string words together to better understand the context.

**2) Determining how current Reddit posts forecase future trends**
- As posts are made in real-time, the context can also differ based on on-going market trends.
- Understanding the market sentiment can be helpful in predicting future trends.

**3) Capturing of image texts**
- While not so for r/investing, >50% of r/wallstreetbets posts are actually images without a message body.
- A majority are meme posts surrounding an ongoing event:
    - *Case in point:* A controversial Peloton advertisement led to a 9% drop in stock price. As a result, there were many meme images and videos posted on r/wallstreetbets. OCR on the images could enable the capturing of new information.
