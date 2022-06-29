# real-fake-tweets
Ml model that classifies whether tweets are real or fake

## Data
In our dataset we have around 23k binary-classified tweets (real/fake), from two different sources (GossipCop ~ 22k, PolitiFact ~ 1k) collected with [FakeNewsNet](https://github.com/KaiDMML/FakeNewsNet).
Our data is slightly unbalanced, 75% of real and 25% of fake news.<br/> In further improvements we can collect additional data, for both fake and real.

## Text preprocessing
There are different possible techniques for preprocessing text. Some of them are: lowercase, keep only alphanumerical values, stemming words, lemmatazing words, removing stopwords and so on.
Concretely our usecase is specific because those steps could clean important differences between fake and real tweets. For pilot version we get the best results when we apply only lowercasing.
<br/>In future we colud definitly try to apply on some part of data the techniques above.

## Split data
Set isn't too big, so we split them to train-test in the following percentage ratio 80%:20%. As well we stratify by target value.

## Count Vectorizer
The computer heavily handle with raw text, so the goal is to pass on some meaningful numbers that represent that text.<br/>
CountVect convert a collection of text documents to a vector matrix. 
First the vocabulary of the words is made, then the words are sorted and assigned an ordinal number.
The sentence is represented as a vector of the vocabulary dimension, so that the i-th coordinate is 1 if the i-th word of the vocabulary is present in the sentence, and 0 otherwise.
This implementation produces computational and memory efficiency sparse matrix.<br/><br/>
For CountVect we used word n-grams, specificly only unigrams which gave us best score. We ignore terms that appear in more than 50% of the documents and in less than 2 documents.

## Linear SVM
For algotihm, we choose Linear Support Vector Machine. SVM is a supervised machine learning model very suitable for text classification problems.
He focuses only at the most difficult examples whereas other classifiers pay attention to all.
The intuition behind SVM approach is that if a classifier is good at the most challenging comparisons, than classifier will be even better at the easy one.
<br/>Two main advantages are higher training speed and better performance with a small and medium datasets, such as text datasets. 
<br/>We try other algorithms too, such as Naive Bayes, Random Forest, XGBoost and so on, but SVM gave us best results on test data.

<br/><br/> <img src="https://github.com/VladimirLukovic/real-fake-tweets/blob/main/SVM_classification_report.png" width="800" height="400">
