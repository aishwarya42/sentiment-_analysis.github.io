
Problem Statement
Conduct sentiment analysis to gauge public opinions on key election-related issues for the year 2024 using tweets related to politics. Analysing the current emotional trend for the ruling party “BJP” among the general public. Identify another impactful party that can alter the public opinion.

What is Text Mining?
Text mining, also known as text data mining, is the process of transforming unstructured text into a structured format to identify meaningful patterns and new insights. You can use text mining to analyze vast collections of textual materials to capture key concepts, trends and hidden relationships.
Text mining is a component of data mining that deals specifically with unstructured text data. It involves the use of natural language processing (NLP) techniques to extract useful information and insights from large amounts of unstructured text data. Text mining can be used as a preprocessing step for data mining or as a standalone process for specific tasks.
What is Sentiment Analysis?
Sentiment analysis is the process of classifying whether a block of text is positive, negative, or neutral. The goal that Sentiment mining tries to gain is to be analysed people’s opinions in a way that can help businesses expand. It focuses not only on polarity (positive, negative & neutral) but also on emotions (happy, sad, angry, etc.). It uses various Natural Language Processing algorithms such as Rule-based, Automatic, and Hybrid.
let’s consider a scenario, if we want to analyze whether a product is satisfying customer requirements, or is there a need for this product in the market. We can use sentiment analysis to monitor that product’s reviews. Sentiment analysis is also efficient to use when there is a large set of unstructured data, and we want to classify that data by automatically tagging it. Net Promoter Score (NPS) surveys are used extensively to gain knowledge of how a customer perceives a product or service. Sentiment analysis also gained popularity due to its feature to process large volumes of NPS responses and obtain consistent results quickly.
Types of sentiment analysis
Sentiment analysis systems fall into several different categories:
•	Fine-grained sentiment analysis breaks down sentiment indicators into more precise categories, such as very positive and very negative. This approach is similar to opinion ratings on a one to five star scale. This approach is therefore effective at grading customer satisfaction surveys.
•	Emotion detection analysis identifies emotions rather than positivity and negativity. Examples include happiness, frustration, shock, anger and sadness.
•	Intent-based analysis recognizes motivations behind a text in addition to opinion. For example, an online comment expressing frustration about changing a battery may carry the intent of getting customer service to reach out to resolve the issue.
•	Aspect-based analysis examines the specific component being positively or negatively mentioned. For example, a customer might review a product saying the battery life was too short. The sentiment analysis system will note that the negative sentiment isn't about the product as a whole but about the battery life.
How Text Mining works ?
Information Extraction -> Data Mining -> Natural Language Processing -> Information Retrieval
•	Information Extraction (IE) – IE is the process of automatically obtaining structured data from unstructured data. This action includes Natural Langauge Processing
•	Data Mining (DM) – Data Mining looks for patterns in data. It can be more described as the retrieval of hidden information from data. Text-Mining in Data-Mining tools can predict responses and trends of the future. It enables businesses to make positive decisions based on knowledge and answer business questions.
•	Natural Language Processing (NLP) – The purpose of NLP in text mining is to deliver the system in the knowledge retrieval phase as an input.
•	Information Retrieval (IR) – IR is considered as an extension to document extraction. IR systems help in to narrow down the set of records that are associated with a specific problem. Text mining involves applying complicated mining algorithms to large-scale documents. By reducing the number of documents, IR can increase the speed of the analysis significantly.
Methodology
Python and R are the most famous text mining tools out there for text mining.
The following steps are to be followed for Text-Mining Python and Text mining in R,
1.	Information Retrieval 
2.	Data Preparation and Cleaning 
3.	Segmentation Tokenization  
4.	Stop-word numbers and punctuation removal  
5.	Stemming  
6.	Convert to lowercase  
7.	POS tagging  
8.	Create text corpus  
9.	Term-Document matrix
About Dataset
The dataset used for this case study is:
“Loksabha Election Tweets 2023”
This dataset compiles a comprehensive collection of tweets related to the Lok Sabha Election in India, scheduled for the year 2024. The dataset encompasses a diverse range of tweets, providing insights into public opinions, sentiments, and discussions surrounding the upcoming political event.
Key Features:
link: This URL corresponds to that specific tweet.
text: Full text of tweets containing election-related tweets.
date: Date and time stamps of when the tweets were posted, enabling temporal analysis.
No_of_likes: This contains the number of likes for each tweet.
No_of_comments: This contains the number of comments for each tweet.
This dataset could be used to analyze the public sentiment before the Loksabha Election 2024.
Only text is used to perform Text Mining to conduct sentiment analysis.
Tokenization
The process of splitting the whole data (corpus) into smaller chunks or smaller words usually single words is known as tokenization (N-Gram model or Bag of words Model)

Stemming and Lemmatization
We do lemmatization in order to prevent data duplication by linking words with the root word. For instance, the words – [big, bigger and biggest] all mean the same and it will cause data redundancy.
install.packages("SnowballC") # for text stemming
library("SnowballC")
TextDoc <- tm_map(TextDoc, stemDocument)

Stop-word numbers and punctuation removal
To go from raw text to fitting a deep learning model. We have to clean the text first, which means – splitting it into words and checking punctuation and case (by converting to lower case).
TextDoc <- tm_map(TextDoc, toSpace, "/")
TextDoc <- tm_map(TextDoc, toSpace, "@")
TextDoc <- tm_map(TextDoc, toSpace, "\\|")
	TextDoc <- tm_map(TextDoc, content_transformer(tolower))
TextDoc <- tm_map(TextDoc, removeNumbers)
TextDoc <- tm_map(TextDoc, removeWords, stopwords("english"))
TextDoc <- tm_map(TextDoc, removeWords, c("s", "company", "team"))
TextDoc <- tm_map(TextDoc, removePunctuation)
TextDoc <- tm_map(TextDoc, stripWhitespace)

Stop Words: The search engine has been programmed to ignore these stop words during indexing entries and retrieving them as the result. Stop words are no use in analytics which will include words like “the”, “a”, “an”, “in”, “is”, “and” etc.

Building the term document matrix
After cleaning the text data, the next step is to count the occurrence of each word, to identify popular or trending topics. Using the function TermDocumentMatrix() from the text mining package, you can build a Document Matrix – a table containing the frequency of words.
TextDoc_dtm <- TermDocumentMatrix(TextDoc)
dtm_m <- as.matrix(TextDoc_dtm)
dtm_v <- sort(rowSums(dtm_m),decreasing=TRUE)
dtm_d <- data.frame(word = names(dtm_v),freq=dtm_v)
head(dtm_d, 5)

The following table of word frequency is the expected output of the head command on RStudio Console.

Plotting the top 5 most frequent words using a bar chart is a good basic way to visualize this word frequent data. 
barplot(dtm_d[1:5,]$freq, las = 2, names.arg = dtm_d[1:5,]$word,
        col ="lightgreen", main ="Top 5 most frequent words",
        ylab = "Word frequencies")
 
One could interpret the following from this bar chart:
•	The most frequently occurring word is “elect”. Also notice that negative words like “not” don’t feature in the bar chart, which indicates there are no negative prefixes to change the context or meaning of the word. ( In short, this indicates most responses don’t mention negative phrases ).
•	“bjp”, “seat” and “congress” are the next three most frequently occurring words, which indicate that people are likely to n=be invested in both the ruling party “bjp” and the opposition party “congress” in the coming elections.
•	Finally, the root “will” is also on the chart which may indicate declaration of any policy or other future endeavours , and it needs further analysis to infer if its context is positive or negative

Generate the Word Cloud
A word cloud is one of the most popular ways to visualize and analyze qualitative data. It’s an image composed of keywords found within a body of text, where the size of each word indicates its frequency in that body of text. Use the word frequency data frame (table) created previously to generate the word cloud.
set.seed(1234)
wordcloud(words = dtm_d$word, freq = dtm_d$freq, min.freq = 5,
          max.words=100, random.order=FALSE, rot.per=0.40, 
          colors=brewer.pal(8, "Dark2"))

Below is a brief description of the arguments used in the word cloud function;
•	words – words to be plotted
•	freq – frequencies of words
•	min.freq – words whose frequency is at or above this threshold value is plotted (in this case, I have set it to 5)
•	max.words – the maximum number of words to display on the plot (in the code above, I have set it 100)
•	random.order – I have set it to FALSE, so the words are plotted in order of decreasing frequency
•	rot.per – the percentage of words that are displayed as vertical text (with 90-degree rotation). I have set it 0.40 (40 %), please feel free to adjust this setting to suit your preferences
•	colors – changes word colors going from lowest to highest frequencies
The word cloud shows additional words that occur frequently and could be of interest for further analysis. Words like “elect”(root for election, elected), “seat”, “leader”. “poll”,”india”, alliance” etc. could provide more context around the most frequently occurring words and help to gain a better understanding of the main themes.
Word Association
Correlation is a statistical technique that can demonstrate whether, and how strongly, pairs of variables are related. This technique can be used effectively to analyze which words occur most often in association with the most frequently occurring words in the survey responses, which helps to see the context around these words.
findAssocs(TextDoc_dtm,terms = c("bjp","congress","rss","bhagwat","gandhi","mahaghathbandhan"), corlimit = 0.6)

 
Sentiment Scores
Sentiments can be classified as positive, neutral or negative. They can also be represented on a numeric scale, to better express the degree of positive or negative strength of the sentiment contained in a body of text.
This example uses the Syuzhet package for generating sentiment scores, which has four sentiment dictionaries and offers a method for accessing the sentiment extraction tool developed in the NLP group at Stanford. The get_sentiment function accepts two arguments: a character vector (of sentences or words) and a method. The selected method determines which of the four available sentiment extraction methods will be used. The four methods are syuzhet (this is the default), bing, afinn and nrc. Each method uses a different scale and hence returns slightly different results.
syuzhet_vector <- get_sentiment(text, method="syuzhet")
head(syuzhet_vector)
summary(syuzhet_vector)

An inspection of the Syuzhet vector shows the first element has the value of 0.00. It means the sum of the sentiment scores of all meaningful words in the first response(line) in the text file, adds up to 0.00 which seems neutral. The scale for sentiment scores using the syuzhet method is decimal and ranges from -1(indicating most negative) to +1(indicating most positive). 
Note that the summary statistics of the suyzhet vector show a median value of 0.00, which can be interpreted as the overall average sentiment across all the responses is neutral.
Next, run the same analysis for the remaining two methods and inspect their respective vectors.
Please note the scale of sentiment scores generated by:
•	bing – binary scale with -1 indicating negative and +1 indicating positive sentiment
•	afinn – integer scale ranging from -5 to +5
bing_vector <- get_sentiment(text, method="bing")
head(bing_vector)

afinn_vector <- get_sentiment(text, method="afinn")
head(afinn_vector)
summary(afinn_vector)

The summary statistics of bing and afinn vectors also show that the Median value of Sentiment scores is 0 and can be interpreted as the overall average sentiment across the all the responses is neutral.
Because these different methods use different scales, it’s better to convert their output to a common scale before comparing them. This basic scale conversion can be done easily using R’s built-in sign function, which converts all positive number to 1, all negative numbers to -1 and all zeros remain 0.
rbind(
  sign(head(syuzhet_vector)),
  sign(head(bing_vector)),
  sign(head(afinn_vector))
)
After binding the results from the 3 methods above the overall average sentiment score turns out to be neutral.
Emotion Classification
Emotion classification is built on the NRC Word-Emotion Association Lexicon (aka EmoLex). The definition of “NRC Emotion Lexicon”, sourced from http://saifmohammad.com/WebPages/NRC-Emotion-Lexicon.htm is “The NRC Emotion Lexicon is a list of English words and their associations with eight basic emotions (anger, fear, anticipation, trust, surprise, sadness, joy, and disgust) and two sentiments (negative and positive). The annotations were manually done by crowdsourcing.”
	d<-get_nrc_sentiment(text)
head (d,10)

The output shows that the fourth line of text has;
•	One occurrence of words associated with emotions of anger, anticipation, disgust and sadness. 
•	One occurrence each of words associated with emotion of joy
•	Two occurrences of words associated with emotions of trust
•	Total of two occurrence of words associated with negative emotions
•	Total of two occurrences of words associated with positive emotions
First, perform some data transformation and clean-up steps before plotting charts. The first plot shows the total number of instances of words in the text, associated with each of the eight emotions. 
td<-data.frame(t(d))
td_new <- data.frame(rowSums(td[2:253]))
names(td_new)[1] <- "count"
td_new <- cbind("sentiment" = rownames(td_new), td_new)
rownames(td_new) <- NULL
td_new2<-td_new[1:8,]
quickplot(sentiment, data=td_new2, weight=count, geom="bar", fill=sentiment, ylab="count")+ggtitle("Survey sentiments")

Next, the following bar chart demonstrates that words associated with the positive emotion of “trust” occurred about five hundred times in the text, whereas words associated with the negative emotion of “surprise” occurred less than 100 times. The negative emotion “anger” occurred 150 times while the positive emotion “joy” occurred more than 150 times. A deeper understanding of the overall emotions occurring in the survey response can be gained by comparing these number as a percentage of the total number of meaningful words.
barplot(
  sort(colSums(prop.table(d[, 1:8]))), 
  horiz = TRUE, 
  cex.names = 0.7, 
  las = 1, 
  main = "Emotions in Text", xlab="Percentage"
)

This bar plot allows for a quick and easy comparison of the proportion of words associated with each emotion in the text. The emotion “trust” has the longest bar and shows that words associated with this positive emotion constitute just over 30% of all the meaningful words in this text. On the other hand, the emotion of “sadness” has the shortest bar and shows that words associated with this negative emotion constitute less than 10% of all the meaningful words in this text. Overall, words associated with the positive emotions of “trust” and “joy” account for almost 40% of the meaningful words in the text. Whereas the words associated with negative emotions of “anger”, “fear”, “sadness” and “disgust” account for almost 34% which can be a sign for change of thoughts among the people about the ruling party in the upcoming general elections 2024. 
In the correlation we see “Congress” still seems to effect the public opinion despite being seen on the periphery. This can lead to huge changes in the election results.
Conclusively, the overall emotions among the people shows both positive and negative signs. Thus, there seems equal polarity neutralising the conclusive win or loss of the ruling party. There seems change among people’s emotions that can lead to surprising results in elections. 
Conclusion
This article demonstrated reading text data into R, data cleaning and transformations. It demonstrated how to create a word frequency table and plot a word cloud, to identify prominent themes occurring in the text. Word association analysis using correlation, helped gain context around the prominent themes. It explored four methods to generate sentiment scores, which proved useful in assigning a numeric value to strength (of positivity or negativity) of sentiments in the text and allowed interpreting that the average sentiment through the text is trending positive. Lastly, it demonstrated how to implement an emotion classification with NRC sentiment and created two plots to analyze and interpret emotions found in the text.


