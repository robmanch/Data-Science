# E-Commerce-Rating-Predictor

## The Problem Statement:

In this project, we will sift through the reviews in our data set and attempt to gauge what sentiment the customer was expressing by trying to predict the rating a customer would give that product.Our project will generate results/insights that may be feed into an e-commerce recommendation system. Recommendation engines then can use this data along with other strategies to make product recommendations to customers. Negative Reviews are to be predicted as matches to the 1-star category and positive reviews as 5-stars.

## The Dataset

To explore the subject further, we chose an interesting dataset with from Kaggle which provided us with real-world data scrapped from a Women’s Clothing E-Commerce Website:
https://www.kaggle.com/nicapotato/womens-ecommerce-clothing-reviews

The data set consists of the following columns:
1.	Clothing ID: Integer variable that refers to the specific piece being reviewed. 
2.	Age: Positive Integer variable of the reviewer's age.
3.	Title: String variable for the title of the review.
4.	Review Text: String variable for the review body.
5.	Rating: Positive Ordinal Integer variable for the product score by the customer [1 Worst, to 5 Best]

## EDA/Preliminary Analysis Report 

### Checking Null Values

![image](https://user-images.githubusercontent.com/62516990/144367434-63e3e774-b118-4bbe-9abd-fcb400e9f314.png)

Observations:
-	Most of the missing values are in the Title and Review Text field. 

### Target Label Distribution 

![image](https://user-images.githubusercontent.com/62516990/144365318-f88a64b3-3c5b-4d88-aeb9-12dbaf12f2d2.png)

Observations:
-	The dataset is highly Imbalanced.
-	It can be seen from the plot that the count of examples for rating 5 is more than 12000 (more than 50%), whereas only 1000 examples are there for a one-star rating.

### Recommend ID and Rating (Target variable)

![image](https://user-images.githubusercontent.com/62516990/144365457-ae71ddff-264d-4827-b6c9-7c5e938ba00b.png)

Observations:
-	This plot shows that the product with higher recommendations tends to have more ratings.

### Word Cloud For Rating 5 

![image](https://user-images.githubusercontent.com/62516990/144365643-dd45553c-6335-4ead-b80d-c58595608ebf.png)

### Word Cloud For Rating 5 

![image](https://user-images.githubusercontent.com/62516990/144365663-9cfd1fd3-e2ac-4666-be07-d8899fa0ac1c.png)

## Feature Engineering:
We created two features, Review_text_len and tile_len, from the features ‘review’ and ‘title’ to look for any correlation of their lengths with the target label.

### Review_text_len and Rating

![image](https://user-images.githubusercontent.com/62516990/144365739-a7e6f96f-8341-4e77-ae49-286a5b232c63.png)

## Data Preprocessing

As we have seen, the dataset contains various features with data types such as categorical, numerical, and text. The ML model, however, can only understand numerical data.

So, we need to convert these features into those that can be understood by the model. The following steps have been taken to tackle this issue:
-	Handling Null Values
-	One hot encoding
-	Min Max Scaling
Text Preprocessing:
-	Removing stop words
-	Regular Expression
-	Lemmatization
-	Merging Title and Review Text columns
-	BOW / TF-IDF

### Strategy to handle Null Values:

-	As we have seen that around 12-13% of data is null in this dataset which is a very large number to drop.
-	We did EDA and found that most of the null index is the same for review text and title.
-	Hence, we merge the review text and title column (explained in feature engineering) and dropped only those rows which have null values for both review text and title.
-	By adopting this strategy, we saved almost 10% of the data.

### One-hot encoding
-	The categorical features ('Division_Name', 'Department_Name', 'Class_Name') in this dataset are nominal, so one-hot encoding is used.
-	After encoding these becomes 29 features in total.

![image](https://user-images.githubusercontent.com/62516990/144366014-00ee1080-ea40-4c09-a88e-60f90a779278.png)

### Min-Max Scaling
-	The features like ‘Age' and 'Positive_Feedback_Count' have their ranges too higher than the encoded features. 
-	This can negatively affect accuracy and training time, so min-max scaling is used to tackle this problem.

![image](https://user-images.githubusercontent.com/62516990/144366125-fb4b2396-7d0c-47a9-938a-ce8533f47b11.png)

### Text Preprocessing

-	The main data features on which we are performing our model is in the form of text which contains strings, symbols, repetitive words, stop words, etc. which are not that useful for our test model, so we performed the data cleaning techniques on these features, 'Title' and 'Review_Text'. 
-	The text needs to be converted to be in such a form that it is easily executable.
-	We performed the following processes on our data.

![image](https://user-images.githubusercontent.com/62516990/144366173-c283153f-519e-4f18-9295-3d492a64bea2.png)

### Removing Stop-words:

-   We used the \'nltk\' library to remove all the stop-words from the
    data and storing the data in an empty list.

### Used Regular Expression:

-   To get every single word from the data we used the regular
    expressions re.sub() method and removed all the Symbols, URLS,
    Punctuations, Next_line character from the available string text and
    converted it to lower case so that we will have a similar kind of
    available data to do further processing.

-   We split the available string into a list of words so that each word
    can be used further.

### Lemmatization:

-   Lemmatization will convert all the available words to their root
    form.

-   E.g.: Words like Happy, Happier, Happiest all will be converted to
    their root form Happy.

-   We performed lemmatization on our list of words after getting the
    data from Regular Expressions and then we join the output to a
    string and our clean data was available for \'Review_Text_Clean\'
    and \'Title_Clean\'.
    
![image](https://user-images.githubusercontent.com/62516990/144366367-5b35d4a9-4b0c-451e-9112-c43e56c6b63c.png)

### BOW / TF-IDF:

-	Our data is still in the form of text after cleaning, we need to convert it to a vector form so that our model can understand the data.
-	To convert our text data into the vector form we used 2 techniques Bag of Words and TF-IDF.

### Bag Of Words:

-	Bag of words creates the vector form for each word available in the 'Review_text' and values it as 0, 1, 2... based on how many times that word is repeated in the Review_Text sentence.

![image](https://user-images.githubusercontent.com/62516990/144366528-0a9e4864-b062-4a4a-9328-eb9db9f26721.png)

-	As you can see the bag of words awards 1 mark to a ‘word count’ each time it encounters a word. Thus, all the words with the same count are treated equally.
-	We are not able to assess which word is most impactful in the sentence, as this approach is more indicative of word quantity than it is of word quality.
-	We do not get a proper/accurate outcome because of this and so moving forward we used TF-IDF in our attempts to tackle this problem.

### TF-IDF

-	TF-IDF is the product of Term Frequency and Inverse Data Frequency.
-	It gives a value to a particular word based on its term frequency in the sentence, so that we can prioritize any word and its impact on the rating properly.
-	Every word with a different priority will have different values as per the word's TF and IDF so that more precise data can be seen than Bag of Words.

![image](https://user-images.githubusercontent.com/62516990/144366604-dbc41fed-7ffd-42a3-a3f2-0278ed2509b3.png)

-	As we can see here every word has different values according to its occurrence in the sentence.
-	After performing all these different methods on our data, we got 10,029 features in our dataset to work upon.

## Feature Extraction
As there is the large number of features, PCA has been tried to reduce the number of features.

![image](https://user-images.githubusercontent.com/62516990/144366700-8cd009f3-28c4-40f0-8e39-fe939289efff.png)

-	2000 principal components are selected as they are giving 90% variance.

![image](https://user-images.githubusercontent.com/62516990/144366740-e313bb86-58ab-4798-b58a-220794d2a9b5.png)

-	Thus PCA is not so great (f1-score = 0.45). Hence, we dropped the idea of feature extraction.

## Modeling Approaches

### Machine Learning Models and hyperparameter tuning

In this study, we use several machine learning algorithms:
1. Logistic Regression
2.  Support Vector Machine with Gaussian Kernel
3.  Support Vector Machine with Linear Kernel
4.  Random Forest

Moreover, we train each model for both BOW and TF-IDF.

## Results & Discussion 

For better understanding and comparison, we created a table with the index as model name and features as evaluation metrics.

![image](https://user-images.githubusercontent.com/62516990/144367047-ddd9da40-45bc-4fb2-b763-5969da53b74d.png)

Note: Some abbreviations are used to make the table more concise:
-	bow: Bag of Words
-	tfidf: TF-IDF
-	lr: Logistic regression
-	rf: Random Forest

## Conclusion

*	Random Forest classifier with TF-IDF vectorizer outperforms the other classifiers.
*	Stratified split provides better results than non-stratified.
*	Feature extraction with PCA didn’t provide good results.

## References

1.	The data is acquired from the following source: Kaggle: https://www.kaggle.com/nicapotato/womens-ecommerce-clothing-reviews
