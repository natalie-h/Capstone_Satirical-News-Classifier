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

In creating a model to classify these articles, the primary metric for evaluation used was accuracy, though to be complete, F1, Precision, Recall, and Brier’s score were also computed for every model used. In running these metrics, it was found across the board that the LSTM model performed the best across all evaluation metrics. On accuracy alone, it outperformed random chance by nearly 40%.

The biggest limitation to this work was the amount of data collected. Because articles are published far less frequently on satirical websites relative to news websites, re-running the scraper would have only produced a few more articles that weren’t duplicates. This model could be vastly improved by collecting data every month to see increased performance. And, as always, additional data cleaning would greatly improve the reliability of the model with removal of extra snippets picked up on by the model and increasing dimensionality of the LSTM model once more articles are acquired.