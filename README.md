# Building a LSTM Neural Network to classify news articles as satirical/genuine

The intention of this project was to build a classifier that could identify whether or not an article taken from the web was from either a known satirical source or a recognized newspaper. 

# Data Collection
Data was collected from an assortment of websites over the course of one week. For article scraping, I used the Newspaper3k library. The only items collected (due to inconsistencies with publication date availabilities) was the URL to the article, the article's title and the text.

To avoid overloading the model with anything that was particularly liberal/conservative in either direction, a small selection of news sources closer to "center" was chosen. That being said, data collection was anything but easy. Since satirical sites don’t have the same number of writers/journalists publishing anything near the volume of genuine news websites, foreign satirical sources were included: The Daily Mash (UK), The Daily Squib (UK), Waterford Whispers News (Ireland), and The Beaverton (Canada). However, to account for spelling differences and the occasional grammatical difference (yes, sometimes English is structurally a little different from country-to-country), the BBC was thrown in to the real news mix. This was a precautionary measure to ensure “favourite” and “colour” wouldn’t interfere with the model as a dead-giveaway.

# EDA
Article clean up was a challenge. The scraper took articles from both 'http://' and 'https://' websites for the same newspapers, so there were many duplicate articles that needed to be deleted. Additionally, some of the articles scraped were purely video or galleries of weekly images. These too needed to be removed from the content. Moreover, I made an executive decision to begin removing certain sections of the newspapers that were less news-oriented and more entertainment-oriented. For example, most Travel sections were eliminated from the genuine sources as well as TV & Entertainment. While I knew that often satirical websites would cover these sections, unless there were a significant number of articles in these sub-sections, I removed them altogether from the newspapers. After removing duplicate and less-relevant articles, I had 1,493 articles total - 658 of which were satirical (44%).

Cleaning up the article text was by far the largest challenge here. To start, I began by removing the HTML using BeautifulSoup. Once completed, I looked at article word lengths for both classes, worried that longer pieces may sway the model in one direction. As expected, the satirical articles were far shorter in length as seen below. To account for this, I truncated the article lengths to 650 words maximum.

Other considerations incorporated were:
- TF-IDF Vectorization.
- Stopwords. 
- Lemmatizing.
- Bi-grams. A few varieties of n-grams were tried out to allow the model to use more than just single words as a consideration. In playing around with these, bi-grams were found to be the strongest.
- Boilerplate text & Self-references. This continued to crop everywhere and had to be removed manually. Examples included "Continue reading the main story" among other phrases. Additionally, a few obvious self-references and phrases such as "The New York Times" and "NYT" had to be removed from the articles.

# Modeling
A number of “simple” models were tried to get an idea of what a baseline in accuracy would be, and for the most part these did fairly well in determining if an article fed to it was from a satirical or genuine source. These included Logistic Regression, Random Forest Classifier, SVM, and Multinomial Naïve Bayes. Each model out-performed random chance, however I decided to try my hand at a neural network.

This is where I developed a LSTM - or long short-term memory - neural network. This is a variation of an RNN that has gates carrying information along in the neural network, in this case: words. LSTM has been demonstrated to be very successful when working with text because it is able to carry over words from the very beginning of a sentence that may be relevant towards the very end.

One quick note about this LSTM model: instead of continuing to use the TF-IDF vectorization in the model itself, I switched over to GloVe word embeddings. By embedding the words we're able to save on both memory that TF-IDF vectorization can't and reduce dimensionality and also use a pre-trained semantic network of words. Given the sparse dataset I already had on hand, I found that using the pre-trained 400,000 words at the 200-dimensional space was sufficient for significant results.

At every metric the LSTM model out-performed the others. However, as the data was limited, early stopping had to be incorporated. Nonetheless, Accuracy capped at roughly 0.84 in the test dataset. 

# Future exploration

Going forward, I'm looking forward to trying this out with additional data. Perhaps adding other foreign sources, including Australian or Indian outlets could provide more insight. That being said, this will require going through these new sources for additional content that may have been accidentally scraped and shouldn't be included. A future endeavor would be to search for any text that may still be present in the articles already included in the dataset with a fine-toothed comb. 

Another area for making this more applicable to other datasets would be to remove generalizations. Many satirical sources are known to include content such as "local man" that can be a dead giveaway to the model.

Adjusting the word counts could also prove interesting; perhaps an area to start would be with how accuracy is affected by a minimum article length.

Finally, I would love to see if the model can perform with a similar accuracy on other mediums. As a starting point, it would be interesting if the headlines could be used for prediction. Eventually it could even be applied to Twitter!

Final presentation:
https://docs.google.com/presentation/d/1_HX7iP-qIrBTAO7aB8DBdLcbq0O_5wuqdBpOUN74tLs/edit?usp=sharing
