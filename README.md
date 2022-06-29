# real-fake-tweets
ML model that classifies whether tweets are real or fake

## Data
In our dataset we have around 23k binary-classified tweets (real/fake), from two different sources (GossipCop ~ 22k, PolitiFact ~ 1k) collected with [FakeNewsNet](https://github.com/KaiDMML/FakeNewsNet).
Our data is slightly unbalanced, 75% of real and 25% of fake news.
<br/><br/> <img src="https://github.com/VladimirLukovic/real-fake-tweets/blob/main/pictures/Target value plot.png" width="700" height="250">
<br/> In further enhancements we can collect additional data, for both fake and real.

## WordCloud
Most common words from real as well as fake tweets you can see in the following pictures:
<br/>
<p float="left">
  <img src="https://github.com/VladimirLukovic/real-fake-tweets/blob/main/pictures/Most common words - real.png" width="500" height="250" />
  <img src="https://github.com/VladimirLukovic/real-fake-tweets/blob/main/pictures/Most common words - fake.png" width="500" height="250" /> 
</p>
By looking at these pictures, we can observe that fake news contains much more celebrity names.

## Text preprocessing
There are many different techniques that can be used for preprocessing text. Some of them are: lowercase, keep only alphanumerical values, stemming words, lemmatazing words, removing stopwords and so on.
Specifically in our usecase, those steps could eliminate important differences between fake and real tweets. For pilot version, we got the best results when we applied only lowercasing.
<br/>In later versions we could apply the abovementioned techniques on specific part of data.

## Split data
Set is not too big, so we split them to train-test in ratio 80%:20%. We stratify by target value as well.

## Count Vectorizer
The machine faces difficulties when it handles with raw text, therefore the goal is to transform text into numbers and use numbers as input for algorithm.<br/>
CountVect converts a collection of text documents to a vector matrix. 
First, the vocabulary of all words is made, then the words are sorted and assigned an ordinal number.
The sentence is represented as a vector of the vocabulary dimension, so that the i-th coordinate is 1 if the i-th word of the vocabulary is present in the sentence, and 0 otherwise.
This implementation produces computational and memory efficient sparse matrix.<br/><br/>
For CountVect we used word n-grams, specifically only unigrams which gave us the best score. We ignore terms that appeared in more than 50% of the documents and in less than 2 documents.

## Linear SVM
We choose Support Vector Machine with linear kernel to be algorithm used in this problem. SVM is a supervised machine learning model very suitable for text classification problems.
It focuses only at the most difficult observations whereas other classifiers pay attention to all data.
The intuition behind SVM approach is that if a classifier is good at the most challenging comparisons, than classifier will be even better at the easy one.
Two main advantages are higher training speed and better performance with a small and medium datasets, such as text datasets. 
<br/><br/>We tried other algorithms as well, such as Naive Bayes, Random Forest, XGBoost etc, but SVM gave us better results.
This is most noticeable for fake tweets in test data, where SVM were better for several percent relative to other algorithms.
<br/><br/>Picture below shows classification report for SVM on train and test data. F1 score will be relevant because we have unbalanced dataset.
<br/><br/> <img src="https://github.com/VladimirLukovic/real-fake-tweets/blob/main/pictures/SVM_classification_report.png" width="600" height="300">
<br/>The results are quite good and do not assume that overfitting or underfitting has occurred. From classification report we can conclude that the model  has more challenges to classify fake tweets than real tweets. That is reasonable because fake tweets are minor class, both in dataset and in real world, and not easy to predict by their form.
<br/><br/> SVM has several hyperparameters to be tuned. For kernel we choose basic type - linear kernel. 
<br/>Linear kernel is mostly prefered for text-classification problems because those problems are usually linearly separated with a lots of features.
In later version we can tuning SVM hyperparameters using Grid Search.
