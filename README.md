# TextInfomationSystems_RacismTextDetector

Overview
The goal of our project is to implement a binary text classification model for
islamophobia, hate against Muslims. In addition to creating the model, we also designed a web
interface for users to input text to see if it is Islamophobic or not. To allow for ongoing data
collection, users can add additional islamophobic comments to the dataset through the user
interface. Lastly, the prevalence of islamophobia from different data sources is visualized in a
dashboard.
Data Collection
We have three data sources: Twitter, Reddit, and YouTube. Twitter data was collected
programmatically through Twitter’s API (link to code to get tweets), Reddit’s API (link to code
to get comments) and YouTube comments were collected manually. Hashtags and @’s were
removed from tweets. Similarly, tweets that clearly came from bots were deleted (daily Quran
recitations). The code to clean the text and to merge the data is here. Table 1 shows how much
data in the preliminary data set came from each data source. This preliminary data set was used
to evaluate the models – the newest data set has 1000 comments total.
We encountered two problems while collecting data. First, Twitter and YouTube have
decent hate-speech detection and censoring algorithms, so the data from those sources are
heavily non-islamophobic. Only 17% of the data is islamophobic. Second, the manual labeling
was very challenging because reading the hateful comments is mentally draining. Coder fatigue
is especially high when the task is focused on something so discouraging.
Picking a Model
We estimated six different text classification models without weights: logistic regression,
linear SVC, multinomial naive bayes, Bernoulli naive bayes, BERT, and Keras (as shown in
Table 2). The models have a binary output (1 if Islamophobic; 0 otherwise. Each model uses
tf-idf for vectorization. To evaluate model performance across the preliminary data set with a
75/25 train-test split, we primarily used macro f1-scores, which are preferable to micro f1-scores
when the data set is as skewed as ours. However, four of the unweighted models (logistic
regression, multinomial naive bayes, bernoulli naive bayes, and BERT) had 0 recall for the
Islamophobic class, which means these models classify everything as not Islamophobic. When
the data set is so heavily skewed, models learn to classify everything as the class that appears
most frequently. To mitigate this, we decided to estimate two weighted models with logistic
regression and linear SVC – none of the other models have built in functionality to add weights.
The weights were designed to be proportional to the class distribution, such that Islamophobic
labels held over four times the weight of non-Islamophobic labels. After adding the weights, the
logistic regression no longer classified all text as not Islamophobic, but linear SVC still performs
better when comparing both the macro- and micro- f1-scores; therefore, we decided to use the
linear SVC model as our final model. Note that the f1-score is still lower than ideal, but given
that hate speech detection is a naturally challenging research area, this is decent as the outcome
of a class project that relies on a small, novel data set.
