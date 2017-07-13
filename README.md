# Yelp-Review-Analysis-using-LDA-MongoDB-Gensim

### Details of the files and implementation: 

yelp/yelp-reviews.py - gets the reviews from the json file and imports them to MongoDB in a collection called Reviews

reviews.py/ reviews_parallel.py - loops through all the reviews in the initial dataset and for each review it: splits the review into sentences, removes stopwords, extracts parts-of-speech tags for all the remaining tokens, stores each review, i.e. reviewId, business name, review text and (word,pos tag) pairs vector to a new MongoDB database called Tags, in a collection called Reviews. If you have many reviews, try running reviews_parallel.py, which uses the Python multiprocessing features to parallelize this task and use multiple processed to do the POS tagging.

corpus.py - loops through all the reviews from the new MongoDB collection in the previous step, filters out all words which are not nouns, uses WordNetLemmatizer to lookup the lemma of each noun, stores each review together with nouns’ lemmas to a new MongoDB collection called Corpus.

train.py - feeds the reviews corpus created in the previous step to the gensim LDA model, keeping only the 10000 most frequent tokens and using 50 topics.

display.py - loads the saved LDA model from the previous step and displays the extracted topics.

predict.py - given a short text, it outputs the topics distribution. Simply lookout for the highest weights on a couple of topics and that will basically give the “basket(s)” where to place the text.

stopwords.txt - stopwords list created by Gerard Salton and Chris Buckley for the experimental SMART information retrieval system at Cornell University
