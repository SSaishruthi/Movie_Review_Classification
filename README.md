# Moview_Review_Classification

Problem Statement
Infer sentiment from free form review text submitted for different movies.

Solution
K-nearest Neighbor Classifier is implemented to predict sentiment for 25000 movie reviews. If it is a positive review, it is represented by ‘+1’ and if it is a negative review, it is represented by ‘-1’

Methodology
1. Splitting train data into review and its corresponding sentiment
2. Data Preprocessing
3. CSR matrix creation and Similarity Calculation
4. Finding ‘K’ nearest neighbor
5. Infer sentiment based on found neighbors

1. Split data
   Before starting data cleaning process, reviews and its corresponding sentiments are separated from the train data set and stored in 
   two different arrays.
2. Data Preprocessing
   In the dataset provided it has been observed that it has HTML tags, numbers, punctuations and characters that are not necessary for 
   analysis. So, the first step is to clean the data. This is the most crucial step of all as they have huge effect on accuracy of the 
   prediction. Following are the data cleaning processes that have been carried out in the data.
   - HTML tag removal: BeautifulSoup is a HTML library for pulling data out of HTML files. It is used to parse content from a html page.      Lxml parser is ranked as the best parser among all in beautifulsoup. So, by this html tags are removed from the reviews and plain        text is obtained.
   - To replace all unnecessary characters other than alphabets, python package ‘re’ is used. This will replace all characters other 
     than alphabets as space.
   - Now the data will have only alphabets but it will be in both upper and lower case. Convert all alphabets to lower case, using    
     ‘.lower()’
   - Stop words such as ‘the’, ‘is’ and ‘are’ are removed using nltk-stopwords module. It will provide list of stop words which can be   
     used as a filter. If words in document are in stopword list then they are moved.
   - Now words are combined to get clean processed data.
   - This is done for both training and testing data.
3. CSR matrix creation and Similarity Calculation
   Text documents are converted into matrix of word counts. ‘TfidVectorizer’ has been used for this purpose. This will create a sparse      representation of the word counts in the document using scipy CSR matrix. Word count is calculated for the entire train and test set.    Obtained CSR matrix is subjected to two processes. First is ‘Inverse Document Frequency’ which will reduce the importance of popular    words and next is ‘Normalization’ which will help in finding cosine similarity in easier way as the denominator will become 1 due to    the process of normalization. There is also an option to select number of features that are to be considered for processing. Ngram is    used to set occurring word in the current window, movement between words are based on n-gram values.
   Model parameters are generated using ‘fit’ and generated parameter from fit is used to generate transformed data set. Cosine    
   similarity is found between generated test and train vectors
4. K-nearest Algorithm
   - Matrix generated from cosine similarity is taken and processed row by row.
   - Arrange columns of every row in the increasing order of similarity and take top ‘k’ indexes and values
   - Match the corresponding review with sentiment using indexes obtained above
   - Group all positives together and negatives together. If number of positives are more than the negative, then the corresponding test      data point will be assigned ‘positive sentiment’ and vice-versa.
   - Output is written into the file.

Selecting ‘K’ value
‘K’ value should be chosen such that outliers do not impact prediction and it should lead to overfitting. General formula for calculating ‘k’ is
K = sqrt(N)
Where, N is the number of data points.
K = sqrt (25000) = 159(approx.)
‘K’ value should be above this, as below this value can increase outlier effect. It should not be increased more as they may lead to overfitting of data points which will increase generalization error,
Random number of features are selected for the processing.
Number of features 9000
K – value 157


ACCURACY - 85.83%
