# Twitter Tweet Sentiment Classification Project

**Author**: [David Boyd](mailto:dboyd580@gmail.com)


## Overview & business problem


90% of all data available is based in text form. It is important as a company to understand how their customers feel about them and what their overall brand perception is, because this additional information can help direct companies to launch new brand marketing campaigns, or could also be a leading indicator towards increased CAC (customer acquistion costs) and a higher likelihood for customer churn if they don't have a positive sentiment about either the brand or the product. A lot of this extra information can be extracted through social media platforms like Twitter via NLP. That is what this project focused on helping to answer.

The goal of this project is to be able to classify tweets based on their contents, which focused primarily on tweets collected related to the SXSW conference.


## Data

The dataset comes from CrowdFlower via data.worldLinks. Human raters rated the sentiment in over 9,000 Tweets as positive, negative, or neither, which can be found in tweets_dataset.csv in the data folder in this repository. The dataset includes 9,092 entries, and 3 columns. Here are the columns in the dataset including our target variable, sentiment

* `tweet_text` - The column contains the contents of the tweet that was captured
* `emotion_in_tweet_is_directed_at` - This column identifies whether the tweet was targeted to a brand or a specific product. There are a lot of NULL values in this column, so it's not super helpful initially
* `is_there_an_emotion_directed_at_a_brand_or_product` - This column helps to identify the sentiment of the tweet

## Method

First I wanted to do some quick EDA to understand what categories are offered in each column and what type of data cleaning I might need to do. After the initial EDA we created several functions to help with the data cleaning stage to get the dataset ready for model building. This involved 

- **Step 1:** Tokenize all tweets
- **Step 2:** Lower case  all tokens
- **Step 3:** Remove all punctuation
- **Step 4:** Remove @mentions
- **Step 5:** html.unescape(text) to remove HTML parsing
- **Step 6:** Remove urls
- **Step 7:** Remove all non asci characters
- **Step 8:** Split attached words
- **Step 9:** Remove common words related to the event itself such as **sxsw**
- **Step 10:** Standardise words (if they use too many letters)
- **Step 11:** Stem/lemmatise words

After the pre-processing stage was complete, we looked at first creating a simple binary classification model, then expanded the model to a multiclassification approach, with the key metric to optimise towards was our `recall score`

## Evaluation

Once the pre-processing stage was complete from above, we can see via a word cloud which words are showing up most frequently for each class. Below is the word cloud for positive sentiment tweets.

![pos-top-words](https://github.com/db495/phase_4_project/blob/main/images/pos-top-words.png)

Below is the top words for the negative sentiment tweets.

![neg-top-words](https://github.com/db495/phase_4_project/blob/main/images/neg-top-words.png)

After evaluating several different transformations and models, with a focus on optimising towards our recall score, we are getting varied results, this could be due to several reasons, however the main one to call out is the fact that the initial dataset is heavily imbalanced towards the neutral tweet compared to the negative sentiment tweets. As a result on all of the models trialled the negative sentiment category always had the lowest results. 



The best performing model on both occassions has been the `CountVectorizer Multinomial Naive Bayes` model

![confusion-matrix](https://github.com/db495/phase_4_project/blob/main/images/confusion-matrix.png)


## Future steps & Limitations

In order to further refine the model in the future, the following limitations need to be addressed:

- Collect more data that allows the class imbalance between categories to be more balanced

Improvements could be made by switching approach from trialling out supervised ML models such as logisitic regression, RandomForest and Multinomial Naive Bayes. Instead it is worth testing out a CNN approach using more advanced techniques such as gensim, GloVe and Word2Vec to help us the hidden layer inside the neural networks to better make the connection between the context of the tweet and the overall sentiment


## For reference
Please find a link to the [presentation here](https://github.com/db495/phase_4_project/blob/main/Tweet%20Sentiment%20Classification.pdf)

You can find a link to the full notebook for my [model here](https://github.com/db495/phase_4_project/blob/main/Sentiment%20Analysis.ipynb)

## Repository Structure

```
├── Data
├── Images
├── README.md
├── Tweet Sentiment Classification.pdf
├── Sentiment Analysis.ipynb
```
