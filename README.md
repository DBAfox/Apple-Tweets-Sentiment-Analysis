# Apple Product Sentiment Analysis

![Apple Logo](/images/Apple_black_white_20240507.jpg)

## by Monica Pecha, Sam Choe, and Daniel Fox

### Overview

This project utilized Natural Language Processing (NLP) to understand the sentiment of Apple products from the 2011 SXSW conference in Austin, Texas. The objective was to build a model that can rate the sentiment of a tweet based on its text.

##
### Business Understanding

Our group was hired as a data advisory group for Apple. Apple is seeking to better understand product sentiment to inform business practices, e.g., how are products received, how are products launched, what product issues are notable, and overall product sentiment.

##
### Data Understanding and Limitations

The dataset comes from CrowdFlower via data.world. The initial dataset contains three features (tweet text, product creator, and human derived sentiment) and 9093 rows regarding both Google and Apple products. 


Limitations include tweets focused on Apple products in relation to the SXSW conference in 2011 and may not be generalizable across non conference participants over time. After VADER sentiment analysis was implemented spot checks indicated that there were several tweets that were not classified correctly. Additionally, the synthetic data generated from ChatGPT produced some words repeatedly, more than we might expect in real life, probably introducing inflated frequencies. 

## Table of Contents

- Exploratory Data Analysis
    - Synthesizing additional data
    - Feature Engineering
    - Implementing VADER
    - Frequencies and Distribution
- Preprocessing
    - Add stopwords, remove punctuation, lowercase all, remove numbers 
    - Tokenizing
    - Vectorizing
        - Count Vectorization
        - Term Frequency - Inverse Document Frequency (Tf-Idf) Vectorization
- Modeling and Evaluating
    - Multinomal Naive Bayes (MNB)
    - Random Forest Classifier (RFC)
    
##
# Exploratory Data Analysis (EDA)

We began our analysis by reading in our data and looking at the rows and columns in our dataframe. We discovered our data was made up of about 9000 tweets from the 2011 SXSW conference. These tweets were directed at either Apple or Google and their respective products. Our data was severly imbalanced but gave us a clear direction to move foreward in.

Its no shock that there are more Neutrals and Positives. People generally tend to tweet Neutrally or Positively. 

![fig0](/images/fig0.png)

Our data was catergorized by human raters but we also have tools for that. we used a technique known as VADER (Valence Aware Dictionary and sEntiment Reasoner) a lexicon and rule-based sentiment analysis tool for natural language processing. its been pretrained on tweets and is the perfect tool to employ here. we also generated tweets to balance out our data for more precise modeling. We then took a sample of each sentiment. 4500 tweets in total

![fig5](/images/fig5.png)
##

Before any modeling we decided to make word clouds of the most frequently used words in each sentiment category.

### Positive

![pos_apple](/images/pos_apple.png)

### Neutral

![neu_apple](/images/neu_apple.png)

### Negative

![neg_apple](/images/neg_apple.png)

We then searched tweets using these top words to come up with our Business Reccomendations showing the tweets to back up our findings 

However we still need to model. With our classes now balanced its time to get into our preprocessing
##
# Pre Processing and Modeling

As always we utilized a train/test split. This ensures that during our process we always have a set of data for or model to learn on and a set that we can evaluate its performance on.

We then set up a wordmap, which sorts every word in our tweets by its part of speech(noun verb, adj, etc)

We also write a function to lemmatize, remove stopwords strip punctuation and change all words to all lowercase. Taking these tweets we instatiate a CountVectorizer and proceeded into our first model. Multinomial Naive Bayes, this model gave us a precision score of 76-77% not bad but you dont just run one model. lets preprocess a bit more and run additional models!

We decided to stick with MNB for a second model but this time instead of a CountVectorizer we employ TF-IDF another vectorizer that not only counts words its specifically gives rarer and more significant words higher scores. we werent sure if this would be a better approach but it was worth a try. This model ended up being 75-76% precise. Again, not bad but its not over!

These models perform much too similarly lets try a different model altogether. W decided on a Random Forest Classifier to try next. We make use of a GridSearch which will find the best hyperparameters for us to tune our model. Since we had two different train/test splits we used both! We ran a model using our CountVectorized data and our TF-IDF sets. While these models took a while to complete they were worth it. Our final model of a CountVectorized Random Forest Classifier was the winner at just under 80% precision.
##

# Reccomendations
 Our reccomendations to Apple are as follows

 1. Increase Battery Life
 2. Continue pop-up stores success
 3. Continue to offer Free products utilize giveaways/raffles etc.

##
# Future Steps
We loved working with Apple and would love to do more analysis as they continue launching products and having conferences. we'd love to gaqin access to the Twitter API to gain more tweet data and provide even more precide models and recomendations.

# Sources
Data provided by CrowdFlower and hosted [here](https://data.world/crowdflower/brands-and-product-emotions)

##
# Navigation

Navigation through our repo is as follows

**Apple Tweets Sentiment Analysis.ipynb**

   Our jupyter notebook  
   Includes findings and recommendations

**Twitter_scraping_template.ipynb**

   second notebook containg code to scrape twitter once access is obtained


**Apple Tweets Sentiment Analysis Presentation.pdf**

   Powerpoint Presentation for this project in pdf format

**.gitignore**

**README.md**

**Data Folder**

   Contains the following data used for analysis 

   * judge-1377884607_tweet_product_company.csv
   * Tweets_SyntheticGeneration_20240503.xlsx

**Images Folder**

   Folder containing images and plots 
   
   * Apple_black_white_20240507.jpg
   * fig0.png
   * fig1.png 
   * fig2.png
   * fig3.png
   * fig4.png
   * fig5.png
   * pos_apple.png
   * neu_apple.png
   * neg_apple.png