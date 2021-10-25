# Stock News NLP
# ![alt text](https://github.com/Eucalyptusss/Stock_News_NLP/blob/main/images_/yahoo_finance_homepage.jpg)
## Project Overview
This repository analyzed the data at retreived from the FMP Cloud API https://fmpcloud.io/.
The goal is to build a classification machine learning model that can accurately predict if a stock will lose or gain value in a given day based on the news being published. In addition to this I was able to derive conclusive modeling technique suggestions for further product development.


## Business Problem
Predicting a stock price is one of the most difficult problems companies are tackling in the machine learning realm. The difficulty is likely because a stock price is determined by the quantity available on the market, i.e. a supply and demand situation. This means that what moves a stock price is the amount of stock units being bought or sold at any given time. If more stocks are being purchased than sold then the existing stock units will increase in price. Stocks are being traded by individuals, stock brokers, hedge funds, entire corporations, and even governments. The amount of variables that determing a stock price make it much more difficult to capture the necessary training data.

## Business Understanding
This leads to my initial proposal of predicting stock price by analyzing a given stock's news headlines/articles. If stock's are determined by how many stocks are being bought or sold then the stock price will have a relationship to public sentiment regarding that stock. This is even more true in the 21st century. By that I mean in the 21st century the people actively trading stocks has shifted strongly in the direction of the general public. Summed up, this is due to being in the age of information. Previously, stocks were traded exclusively by insiders or people with some form of connection to the market. Now, anyone with internet access and a bank account can invest. Using stock news to predict the stock's gain/loss for a given day will surely not be the only metric needed to predict, but investigating how precise the following models are could prove to be well worth it.
# Process
  1. Preprocess Data
  2. Explore Data
  3. Develop models
  4. Optimize, validate, finalize, and analyze models
  5. Determine relevant business results
  6. Provide evidence for business conclusions

# Preprocessing 
  1. Obtain stock news for a provided list of stock symbols with a ticker parameter denoting how many stock news object to retrieve.
  2. Add the following features:
      - Boolean : is_weekday
      - Int : weekday (0 == Monday)
  3. Obtain actual stock data from the stock_news dataframe after extracting stock symbols & date range of stock news.
  4. Combine actual stock data with stock news in the following format:
      - Models predict binary outcome of change where change is stock_open - stock_close
      - News is classified as 'gain' if change at the end of the corresponding prediction date > 0 otherwise 'loss'
      - Stock news between 16:00 and 24:00 will predict stock change on the following business day.
      - Stock news between 00:00 and 16:00 will predict stock gain/loss on the same day.
  5. From here two methodologies were developed.
    1. Predict stock gain/loss based on sentiment scores provided by the VADER sentiment analysis within NLTK
        - Determine sentiment scores for title & text of a news object
        - Train model with ONLY sentiment scores not text
    2. Predict stock gain/loss using natural language processing techniques
        - Combine text & title
        - Count max text length & unique words
        - Tokenize and remove puncuation
        - Sequence into same sized sequences
        - Add word embedding from GloVe model (https://nlp.stanford.edu/projects/glove/)
        - Train model using only embeded text 
#### In the visualization below note that there does not exist stock data where there is not news regarding the stock.
![alt text](https://github.com/Eucalyptusss/Stock_News_NLP/blob/main/images_/data_viz.png)
        
# Modeling
#### I developed 5 distinct models. Please note, each time a model is trained a random set of stock symbols is analyzed. Meaning, that the below model metrics are only a general representation.

1. Vader Sentiment Model
  - Does not use machine learning
  - Predictions are based on the Comound Average Score of text and title i.e. >0 predicts gain <0 predicts loss
  - ![alt text](https://github.com/Eucalyptusss/Stock_News_NLP/blob/main/images_/baseline_vader_sentiment.png)

2. XGBOOST using Vader Sentiment Scores
  - Superivised Machine Learning
  - Uses vader  sentiment scores to predict gain/loss of a given stock
  - ![alt text](https://github.com/Eucalyptusss/Stock_News_NLP/blob/main/images_/baseline_xgboost.png)
  
3. Recurrent Neural Network using GRU layer
  - Superived Machine Learning
  - GloVe word embedding entry layer
  - Uses text contained in title and body of retreived news object
  - ![alt text](https://github.com/Eucalyptusss/Stock_News_NLP/blob/main/images_/recurrent_nn_GRU.png)
  
4. Recurrent Neural Network using LSTM layer
  - Supervised Machine Learning
  - GloVe owrdd embedding layer
  - Uses text contained in title and body of retrived news object
  - ![alt text](https://github.com/Eucalyptusss/Stock_News_NLP/blob/main/images_/recurrent_nn_LSTM.png)


# Conclusions
1. Develop & Patent NLP process to further understand stock news. Spend equal resources on processing text & body.

2. Class imbalance should be dealth with in the following way, ratios on the lower end of the spectrum e.g. < 8 should use skearn generated weights. While, class imbalance rations on the higher end < 8 should use the average weight between sklearn and the general forumula loss/gain.

3. Transformers models are the best in class for Natural Lanugage Processing, when developing models use a vanillas transformer as the baseline to ensure product value.

# Author

Please reach out to me at:
https://www.linkedin.com/in/vincent-404/
or email me at:
jvincentwelsh99@hotmail.com
