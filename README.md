# nlp_project

The deliverable consists of environment code, preprocessing/splitting the data and algorithms. 
Introduction
With exponential growth of social media channels and the ease of sharing thoughts and suggestions online created an enormous pool of data on the humankind. Twitter has 48.35 million monthly active users only in the United States. In the world where knowledge is power, natural language processing acts as an enabler to translate raw data into valuable intelligence on people and their responses to the range of events from everyday routine to major life events.  
NLP is developing daily but still faces challenges when interpreting sentiments intended by the speaker or writer. Since the humans tend to use complex expressions where the emotion attached to a word or word combination might have variations based on the words coming before or after that specific word. That leads to my research topic in which I have a personal interest. In this project I would like to work on a social media dataset to identify the overall mood of a tweeter input also knows as “tweet”. So, the question I propose to tackle is what is overall sentiment attached to a tweet? 
Literature Review
To prepare for this project, I reviewed numerous research papers and web articles as the field is developing pretty fast and new approached get created for better and more accurate machine training.   
Bing Liu’s book on Sentiment Analysis and Opinion Mining provides general introduction into the subject of sentiment analysis. Moreover, the majority of other articles reviewed afterward refer to Bing Liu’s work. The book covers all important topics and development. This was an excellent reference for the purpose of my project to provide basic idea on the problem.
Federico Alberto Pozzi’s book Sentiment Analysis in Social Networks builds on social network setting for sentiment analysis. It describes several challenges and solution approaches on handling figurative language devices such as irony and sarcasm that might not always be evident for non-humans.  
Anastasia  Giachanou & Fabio  Crestani’s article Like It or Not: A Survey of Twitter Sentiment Analysis Methods narrows down the focus to Twitter platform only. Several approaches are discussed in the article as well as other Twitter-related analysis.  
Dataset
For the purpose of the project, open-source tweeter dataset was used which contains 1,584,465 unique tweets. The attributes in the dataset are: 
•	Target: polarity of the tweet. “0” is negative and “1” is positive. Neutral responses were omitted by the publisher of the dataset. 
•	ID: identification number od the tweet within Tweeter API. 
•	Date: the date of the tweet. 
•	Flag: unknown purpose 
•	User: username of author of corresponding tweet
•	Text: tweet content
Out of six attributes, only two were left for the main research dataset: target and text because the research question looks into the language component. There may be cases where the timing or specific user maybe correlated with the overall sentiment of the tweet however for this project, I assume that omitted attributes do not contribute to the outcome. Another thing to note about the dataset is that emoticons were removed by the publisher. Target variable was renamed as sentiment. 
The dataset is balanced where approximately 50% are negative tweets and 50% of positive. There are 786,609 mentions and abundance of hashtags that are specific to social media posts. The most frequently used hashtags are #followfriday, #fb, and  ##squarespace
Descriptive stats for textual data: 
	BEFORE PREPROCESSING 
Lexicon count 	20,859,449
Readability (using Flesch reading ease formula)	54.39
Grade level (using smog index)	11.6
Approach
After reviewing numerous works on NLP, the following approach was decided to be taken. As the data structure is fairly simple with only 2 variables, there was no need for cleaning the data for missing values and such before exploratory analysis. It followed by NLP preprocessing to get textual data ready for further analysis and model building. The approach diagram can be found below: 
 
Step 1: Descriptive Analysis
The first step was to get the clear view of the dataset and the following step were taken: 
•	Plotted sentiment distribution. 
•	Conducted linguistic analysis of the data such as readability and lexicon capacity: 
•	Found average number of word and characters per tweet. 
•	Checked for any correlation between length of tweet and its labeled polarity: negative tweets tend to be insignificantly longer than positive ones. 
Step 2: Data Preprocessing
These are the steps processed to standardize the text dataset:  
•	Replaced all links with "URL”. 
•	Substituted mentions with "USER". 
•	Removed non-alphabetic characters such as commas, dots etc. 
•	Shortened repeating letters with two of the same letters.  
•	Removed stopwords.  
•	Applied lemmatization. 
•	Applied TF-IDF Vectorizer. 
Step 3: Building Classifier  
•	Logistic regression model 
•	Naïve-Bayes Model 
•	Basic Neural Network
Step 4: Post-Predictive Analysis 
•	Topic modeling
Results
The detailed approach accompanied by the respective programming can be found on the GitHub page: https://github.com/nbunaeva/nlp_project/blob/master/CapstoneInitialResults.ipynb
The results of exploratory analysis: it was found that the data labels are equally distributed and there is no imbalance in the data. Average number of characters is equally distributed, however there is an insignificant difference when it comes to average number of words per tweet where negative tweets tend to have a slightly larger average. 
  
Correlation matrix did not indicate any significant correlation between number of words/characters and polarity of tweets. 
  
The first classification algorithm used for predictive modeling was Naïve Bayes Model with Bernoulli distribution. It showed similar results with the second algorithm used which was Logistic Regression. Both models were able to yield accuracy of 75-76%, precision between 74-76% and recall from 73% to 77%. Logistic regression showed insignificantly better result compared to Naïve Bayes.  Analysis of the confusion matrix did not indicate significant skewness of the algorithms, where the difference between False Negatives (11.53%) and False Positives (13.31%) is under 2%. As a general trend, both models are insignificantly skewed to label tweets as positive with 51.8% positive rate. 
Model name		Precision 	Recall	F1-score	Support
Logistic Regression 	Negative Tweets	0.78	0.73	0.75	39989
	Positive tweets	0.75	0.79	0.77	40011
	Accuracy 			0.76	
Naïve Bayes Model 	Negative Tweets	0.76	0.73	0.75	39989
	Positive tweets	0.74	0.77	0.75	40011
	Accuracy			0.75	
The third model, Basic Neural Network, produced only 68.45% accuracy which falls far behind previously discussed methods. 
After reviewing the result that were not completely satisfactory, it was decided to process further data preprocessing. From the below word clouds, it can be seen that the most frequently used word in both categories is USER as this is the substitute for tweets mentions. After removing the words from the dataset, the model results did not significantly change. 
The other step taken to get better results was the reduction of number of stops words as some of the omitted words could be useful for polarity detection such as ‘unfortunately’, ‘sadly’ etc. The word clouds for the new dataset look like this: 
  

The transformation showed good results with 4-5% accuracy increase.  Naïve Bayes remains skewed towards positive tweets whereas Logistic Regression shows more equally weighted results. Remarkable increase was attained in recall for negative tweets for the regression model of 7% which means that there were more actually negative tweets identified correctly. This is related to the fact that the stopwords used for the first model removed large number of negative words: 
Model name		Precision 	Recall	F1-score	Support
Logistic Regression 	Negative Tweets	0.82 (+4%)	0.80 (+7%)	0.81 (+6%)	39989
	Positive tweets	0.81 (+6%)	0.82 (+3%)	0.82 (+5%)	40011
	Accuracy 			0.81 (+5%)	
Naïve Bayes Model 	Negative Tweets	0.81 (+5%)	0.76(+3%)	0.78 (+3%)	39989
	Positive tweets	0.77 (+3%)	0.82(+5%)	0.80 (+5%)	40011
	Accuracy			0.79 (+4 %)	

For post-predictive analysis, topic modeling techniques were applied.
Topic modeling revealed the following topics based on common words. It took human interpretation to generalize the themes. 
	Key Words 	Common Theme
Topic 0:
	user yeah haha hope aww hey follow nice awesome cool	Feel good 
Topic 1:
	good morning night luck feel hope sound thing lost feeling	Morning greeting
Topic 2:
	work tomorrow ready hour tired weekend week tonight 
wanna sleep	Workweek struggle
Topic 3:
	url check cute pic add photo follower video gt amp	Sharing media files 
Topic 4:
	quot song amp watching movie thing haha people tweet 
friend	Movie night
Topic 5:
	day happy great mother tomorrow school hope nice long beautiful	Mother’s day greeting
Topic 6:
	love song haha guy amp friend watching movie life happy	Happy romance 
Topic 7:
	lol haha yeah twitter dont aww feel amp fun bad	Emotions
Topic 8:
	today feel feeling sick school sad hope fun bad gonna	Missing school while sick
Topic 9:	time night sleep twitter bed great fun tomorrow tonight long	Night greeting

When topic frequency distribution was drawn, it can be seen that Emotion and Feeling good themes significantly more frequent than other themes. 
  
Interestingly, frequency distribution is not drastically different when data is split by sentiment. That mean that both negatively and positively labeled tweets contain key words from all topics. It is worth to note that Happy Romance is seen more frequently in negative tweets. 
  
Conclusions
Tweeter as a social media network has a wide representation in different socio-economical groups thus creating a large amount of data, where the challenge is in preprocessing and filtering the date for further analysis.
There is a certain complexity in analyzing social media datasets in a general context where the textual data can be short and taken out of a conversation. Even working with such data, satisfactory results of 80% accuracy were obtained using basic algorithms. It has been proven in this project that data preprocessing is the key and simple thing as a proper list of stopwords can drastically improve performance of a model. 
The possible used of NLP on Tweeter data are wide ranging from small companies trying to build their name while trying to see the target market response to marketing campaigns all the way to assessing public response to major event such  as policy and law changes. 


