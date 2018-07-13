# Capstone_Satirical-News-Classifier

The intention of this project was to build a classifier that could identify whether or not an article taken from the web was from either a known satirical source or an actual newspaper. Data was collected from an assortment of websites over the course of one week:
- The New York Times
- CNN
- Fox News
- NBC News
- The BBC *
- The New Yorker (Borowitz Report)
- The Onion
- Clickhole
- Make America the Best
- The Skunk
- Islamica News
- Babylon Bee
- The Valley Report
- The Beaverton *
- Waterford Whispers News *
- The Daily Squib *
- The Daily Mash *
An * indicates a non-American source

Given the limited availability of satirical articles, the dataset was expanded to include articles from Canada, the UK, and Ireland. To account for spelling changes, the BBC was included as a source for news articles as well.

With the strongest model (LSTM), accuracy was roughly 0.84; given that baseline accuracy was approximately 0.44, this was a very strong predictor of whether or not an article was from a satirical source. Additionally, the F1, Precision, Recall, and Brier’s score all indicated that this was the strongest model as well - with the RNN scoring about 10 points greater on each evaluation metric relative to the other models (Logistic Regression, Random Forest, SVM, and Multinomial Naïve Bayes).

The biggest limitation to this work was the amount of data collected. Because articles are published far less frequently on satirical websites relative to news websites, re-running the scraper would have only produced a few more articles that weren’t duplicates. This model could be vastly improved by collecting data every month to see increased performance. And, as always, additional data cleaning would greatly improve the reliability of the model with removal of extra snippets picked up on by the model and increasing dimensionality of the LSTM model once more articles are acquired.