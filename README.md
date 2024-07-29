# NLP-tweet-sentiment-project

![image](https://github.com/user-attachments/assets/c87df5b6-02ad-46f5-acd7-6c420e6dab15)


### BUSINESS OVERVIEW:

Brand and Product Emotions refer to the feelings and attitudes that consumers express towards specific brands and their products. These emotions, which can be positive, negative, or neutral, are influenced by factors such as personal experiences, marketing efforts, product quality, and social trends. We can offer useful insights for enhancing customer satisfaction and brand reputation by categorizing the emotions conveyed in tweets and identifying the targeted brands or items. Social media sentiment has a big influence on how consumers perceive brands and behave. Negative attitudes can cause reputational harm and consumer attrition, while positive sentiments can increase brand loyalty and draw in new clients. As a result, Codel Electronics Company's marketing department must track and evaluate public opinion to proactively fix problems and capitalize on favorable comments for advertising

### Stakeholder

Codel Electronics brand Manager who is responsible for overseeing the brand's image and reputation, ensuring it aligns with the company's values and market goals


###  PROBLEM STATEMENT

Codel Electronics Company lacks comprehensive insights into consumer emotions and public opinion towards its products and brands. This hinders their ability to identify areas for improvement, enhance customer satisfaction, and develop effective market strategies. A systematic approach to analyzing Twitter sentiment is needed to gain actionable insights and stay competitive.

### OBJECTIVES:

**MAIN OBJECTIVE**

To develop predictive models to classify the sentiment (positive, negative, or neutral) expressed in tweets about brands and products.

**SPECIFIC OBJECTIVES**
To leverage Twitter data to manage and comprehend public opinion about Google and Apple products brands offered by Codel Electronics

To identify the best-performing product, in terms of positive and negative

To understand sentiment (emotion) distribution regarding Apple and Google brand

To provide actionable insights from analyzing Twitter sentiments

### SUCCESS CRITERIA

Goal: Creating a multiclass machine learning mode with an accuracy of more than 75% and a f1_score of more than 70%


### CONSTRAINTS

. High computational needs are required when tuning and optimizing our models

. Quality of data -The Target variable has a huge class imbalance

  ## Data Understanding

 The dataset comes from CrowdFlower via data. world [Source](https://data.world/crowdflower/brands-and-product-emotions), It contains  3 columns with over 9000 tweets of people's  sentiments about Google and Apple products on Twitter which were classified as either positive, negative, no emotions, or. I can't tell


#### Features(columns)
1. **Tweet_text (Categorical)**: The text of the tweet. This feature contains the actual tweet content posted by users, it's also our predictor variable
   
2. **Emotion_in_tweet_is_directed_at (Categorical)**: The brand or product that the emotion in the tweet is directed at. This feature identifies which brand or product is the target of the emotion expressed in the tweet.
   
3. **Is_there_an_emotion_directed_at_a_brand_or_product (Categorical)**: Indicates whether there is an emotion directed at a brand or product. The possible values include "Positive emotion", "Negative emotion", and "No emotion toward brand or product", which is also our target variable

### Data Importation and Inspection

#### First 5 Rows:
The dataset comprises tweets about multiple brands and products, along with emotions directed towards them.

#### Basic Data Information:
The dataset has 3 columns:
1. `tweet_text`: Contains the text of the tweet.
2. `emotion_in_tweet_is_directed_at`: Indicates the brand or product the emotion is directed at.
3. `is_there_an_emotion_directed_at_a_brand_or_product`: Specifies whether there is a positive, negative, or no emotion directed at the brand or product.

- The dataset has a total of 9093 entries.
- The `tweet_text` column has 9092 non-null values.
- The `emotion_in_tweet_is_directed_at` column has 3291 non-null values.
- The `is_there_an_emotion_directed_at_a_brand_or_product` column has 9093 non-null values.

#### Data Shape:
The dataset consists of 9093 rows and 3 columns, indicating there are 9093 observations and 3 features.

#### Data Types:
- All three columns (`tweet_text`, `emotion_in_tweet_is_directed_at`, and `is_there_an_emotion_directed_at_a_brand_or_product`) are of object type, indicating they contain categorical or text data.

#### Summary Statistics:
The summary statistics provide insights into the distribution of data in the dataset.

- **tweet_text**:
  - **Count:** 9092 (total observations)
  - **Unique:** 9065 (unique tweets)
  - **Top:** "RT @mention Marissa Mayer: Google Will Connect You With The Future!" (most frequent tweet)
  - **Frequency:** 5 (occurrences of the most frequent tweet)

- **emotion_in_tweet_is_directed_at**:
  - **Count:** 3291 (non-null observations)
  - **Unique:** 9 (unique brands/products)
  - **Top:** "iPad" (most frequent brand/product)
  - **Frequency:** 946 (occurrences of the most frequent brand/product)

- **is_there_an_emotion_directed_at_a_brand_or_product**:
  - **Count:** 9093 (total observations)
  - **Unique:** 4 (unique sentiment categories)
  - **Top:** "No emotion toward brand or product" (most frequent sentiment)
  - **Frequency:** 5389 (occurrences of the most frequent sentiment)

These statistics are useful for understanding the data distribution and identifying any potential inconsistencies or areas for further investigation. The dataset provides a solid foundation for analyzing public sentiment towards brands and products based on Twitter data.

## Data Preparation

### Data Cleaning

**Steps to be followed**
1. **Completeness**
 checking for missing values and handling them

 We dropped one null value from the 'tweet-text' column  

2. **Consistency**  -

checking for duplicate values and handling them
  
we dropped  duplicates because they appeared to be caused by  hashtags and the repetition of tweets

3. **Uniformity**
   
we will rename our columns as well as clean our texts by removing punctuations capital letters, numbers, white spaces,@ symbols as well as  hashtags and change the "no emotions towards brand' emotion to 
neutral emotion for  easy interpretability

4. **Tokenizing**
  
Tokenize our tweets these will enable the machine to process our text data

5. **Removing of stop words**

Removing  stopwords helps to shorten our texts for easy processing and modeling as well as removing irrelevant words that will affect our modeling
 
6. **Normalization** -

Through lemmatization so as to retain  most of the information and meaning of the words
   
### Feature engineering

Adding a company_name column which enables us to view the different products mentioned in the tweets either there from Apple or Google

## EDA and Visualization
#### Univarent analysis

**A barplot of distribution of 'emotion' (target variable)**

![image](https://github.com/user-attachments/assets/c8baf427-10cf-4675-a0a5-e3c964c85ecb)

**Observation**

- The most frequently occurring emotion is `Neutral emotion`, with a count of  more than 5000, followed by positive emotion with more than 2500 counts. Negative emotions with more than 500 counts and finally I can't tell with below 200 counts.

- There is a noticeable disparity between the counts of No emotion toward brand or product (5338) and the other emotions, with Positive emotion being the next most frequent at 2527, and Negative emotion at 570.


- The high frequency of No emotion toward a brand or product might be attributed to users sharing informational or factual content about the products rather than personal opinions or emotional responses.

- A huge class imbalance between the classes

 **A histogram visualizing the lemmatized_tweet column**

![image](https://github.com/user-attachments/assets/25eec3d2-5005-4fb4-bbcf-b243e0246938)

**Observation**

The histogram shows that news `lemmatized tweets` range from 10 to 140 characters  

There appears to be a normal distribution

**A histogram to visualize the average length of words in Google and Apple products tweets**

![image](https://github.com/user-attachments/assets/048ad3e1-e96c-4ce6-847c-3aec10b49d62)

**Observation**

The histogram shows that the average word length in these tweets is  5 words, with most tweets falling within the range of 4-5.

#### Bivarent Analysis

**Most frequent Bargrams used in the dataset**

![image](https://github.com/user-attachments/assets/ead876b2-4c24-4c53-9fa2-cfe9cafe0f2f) 

**Observation**

We can observe that the bigrams such as `Apple store` are mostly related to  dominating the Google and Apple products tweets. Bigrams such as "rt mention" dominating the dataset suggest that many tweets are retweets or mentions, typically used to highlight trending topics, news, and user opinions. This can imply that discussions about Apple and Google products are significantly influenced by social sharing and user interactions on the platform

**A bar plot showing the top positive and negative sentiments**

![image](https://github.com/user-attachments/assets/d05ba5c7-d52e-4fde-85f3-0dda226c8821)

 **Observation**

Analyzing the most frequent words in positive tweet sentiments reveals interesting insights into customer sentiment toward Apple and Google products. For instance, words like `iPad and Google` dominate positive sentiments towards Apple, indicating a strong appreciation for its
On the other hand, positive tweets about Google frequently feature words like `google`  This analysis helps google and Apple to understand the specific aspects that drive positive sentiment for each brand, enabling them to tailor marketing strategies and product recommendations accordingly. 

![image](https://github.com/user-attachments/assets/bdcc943c-152b-4ef9-94d4-c8b62d89ce1a)


**Observation**

Negative sentiment analysis reveals frequent words like `ipad, iphone, and google` indicating customer dissatisfaction with product pricing, performance issues, and potential usability concerns for certain Apple and Google devices.

## Modelling and Evaluation

### Why Binary and Multiclass Classification?

#### Binary Classification
We decided to perform binary classification to distinguish between 'Positive emotion' and 'Negative emotion.' This task simplifies the problem and focuses on detecting the polarity of sentiments, which is crucial for applications like customer feedback analysis, where identifying positive or negative sentiments can be directly actionable.

#### Multiclass Classification
We expanded to multiclass classification to include 'Neutral emotion' along with 'Positive emotion' and 'Negative emotion.' This task provides a more nuanced understanding of the sentiments expressed in the tweets, allowing for a more comprehensive sentiment analysis. This is particularly useful in social media monitoring and understanding public opinion, where not all sentiments are purely positive or negative.

### Binary Classification

#### Models Used
1. **Logistic Regression**
2. **Gaussian Naive Bayes**
3. **Random Forest Classifier**

#### Metrics for Evaluation
- **Accuracy**: Measures the overall correctness of the model.
- **Precision**: The proportion of true positive predictions among all positive predictions. Important for assessing the quality of positive predictions.
- **Recall**: The proportion of true positives correctly identified. Important to understand the ability of the model to capture all positive instances.
- **F1-Score**: The harmonic mean of precision and recall. Provides a balance between precision and recall.
- **ROC AUC**: Measures the model's ability to distinguish between classes. A higher AUC indicates better performance.

#### Results
After tuning and evaluating the models, the following results were obtained:

| Model                   | Accuracy | Precision (Positive) | Recall (Positive) | F1-Score (Positive) | ROC AUC |
|-------------------------|----------|----------------------|-------------------|---------------------|---------|
| Logistic Regression     | 0.85     | 0.93                 | 0.89              | 0.91                | 0.87    |
| Gaussian Naive Bayes    | 0.85     | 0.91                | 0.91              | 0.91                | 0.83    |
| Random Forest Classifier| 0.86    | 0.89                 | 0.95              | 0.92                | 0.82    |

**Best Model for Binary Classification**: The **Random Forest Classifier** demonstrated the highest accuracy (86%) and ROC AUC (0.82), making it the best-performing model for the binary classification task. This model balances precision and recall effectively, providing a robust classification performance.

### Multiclass Classification

#### Models Used
1. **Multinomial Naive Bayes**
2. **Gradient Boosting Classifier**
3. **Voting Classifier**
4. **Stacking Classifier**

#### Metrics for Evaluation
- **Accuracy**: Measures the overall correctness of the model.
- **Precision**: The proportion of true positive predictions among all positive predictions for each class.
- **Recall**: The proportion of true positives correctly identified for each class.
- **F1-Score**: The harmonic mean of precision and recall for each class.
- **ROC AUC**: Measures the model's ability to distinguish between classes for each class. A higher AUC indicates better performance.

#### Results
After tuning and evaluating the models, the following results were obtained:

| Model                  | Accuracy | Precision (Macro Avg) | Recall (Macro Avg) | F1-Score (Macro Avg) | ROC AUC (Macro Avg) |
|------------------------|----------|-----------------------|--------------------|----------------------|---------------------|
| Multinomial Naive Bayes| 0.64     | 0.52                  | 0.50               | 0.51                 | 0.62                |
| Gradient Boosting      | 0.63     | 0.57                  | 0.55               | 0.56                 | 0.68                |
| Voting Classifier      | 0.68     | 0.60                  | 0.61               | 0.60                 | 0.70                |
| Stacking Classifier    | 0.68     | 0.60                  | 0.61               | 0.60                 | 0.70                |

**Best Model for Multiclass Classification**: Both the **Voting Classifier** and **Stacking Classifier** showed similar performance, with an accuracy of 68% and a macro average ROC AUC of 0.70. These models balance precision, recall, and F1-score effectively across all classes.

### Rationale for Metric Choices
- **Accuracy**: Provides a straightforward measure of overall model performance but can be misleading in the presence of class imbalance.
- **Precision and Recall**: Important for understanding the trade-off between the number of false positives and false negatives. Critical in applications where either false positives or false negatives carry a high cost.
- **F1-Score**: Balances precision and recall, making it a suitable metric when we need to find a balance between the two.
- **ROC AUC**: Measures the model's ability to distinguish between classes, providing a comprehensive view of model performance across different thresholds.
