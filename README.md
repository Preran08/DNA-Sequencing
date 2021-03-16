# DNA-Sequencing Using NLP
### Using the human.txt dataset from Kaggle 
![Screenshot (33)](https://user-images.githubusercontent.com/38466518/111237008-8703e700-85ca-11eb-8cf1-9759c18b5b70.png)
### We have some data for human DNA sequence coding regions and a class label.  We also have data for Chimpanzee and a more divergent species, the dog.


### Here are the definitions for each of the 7 classes and how many there are in the human training data.  They are gene sequence function groups.
![Screenshot (31)](https://user-images.githubusercontent.com/38466518/111237050-92571280-85ca-11eb-9cba-5b31ef6f890b.png)

### Treating DNA sequence as a "language", otherwise known as  k-mer counting

A challenge that remains is that none of these above methods results in vectors of uniform length, and that is a requirement for feeding data to a classification or regression algorithm. So with the above methods you have to resort to things like truncating sequences or padding with "n" or "0" to get vectors of uniform length.

DNA and protein sequences can be viewed metaphorically as the language of life. The language encodes instructions as well as function for the molecules that are found in all life forms. The sequence language analogy continues with the genome as the book, subsequences (genes and gene families) are sentences and chapters, k-mers and peptides (motifs) are words, and nucleotide bases and amino acids are the alphabet. Since the analogy seems so apt, it stands to reason that the amazing work done in the natural language processing field should also apply to the natural language of DNA and protein sequences.

The method I use here is simple and easy. I first take the long biological sequence and break it down into k-mer length overlapping “words”. For example, if I use "words" of length 6 (hexamers), “ATGCATGCA” becomes: ‘ATGCAT’, ‘TGCATG’, ‘GCATGC’, ‘CATGCA’. Hence our example sequence is broken down into 4 hexamer words.

Here I am using hexamer “words” but that is arbitrary and word length can be tuned to suit the particular situation. The word length and amount of overlap need to be determined empirically for any given application.

In genomics, we refer to these types of manipulations as "k-mer counting", or counting the occurances of each possible k-mer sequence. There are specialized tools for this, but the Python natural language processing tools make it supe easy.

### Next we will define a function to collect all possible overlapping k-mers of a specified length from any sequence string. We will basically apply the k-mers to the complete sequences

![Screenshot (32)](https://user-images.githubusercontent.com/38466518/111237645-e6162b80-85cb-11eb-95f6-065f9d1ac1e7.png)

### Since we are going to use scikit-learn natural language processing tools to do the k-mer counting, we need to now convert the lists of k-mers for each gene into string sentences of words that the count vectorizer can use.  We can also make a y variable to hold the class labels

## Now we will apply the BAG of WORDS using CountVectorizer using NLP
### If we have a look at class balance we can see we have relatively balanced dataset.

![Screenshot (35)](https://user-images.githubusercontent.com/38466518/111237029-8c613180-85ca-11eb-8a3c-f095c0237810.png)

### A multinomial naive Bayes classifier will be created.  I previously did some parameter tuning and found the ngram size of 4 (reflected in the Countvectorizer() instance) and a model alpha of 0.1 did the best.

MultinomialNB(alpha=0.1, class_prior=None, fit_prior=True)

### Looking at some model performce metrics like the confusion matrix, accuracy, precision, recall and f1 score.  We are getting really good results on our unseen data, so it looks like our model did not overfit to the training data.

![Screenshot (28)](https://user-images.githubusercontent.com/38466518/111237833-45743b80-85cc-11eb-9a32-77abc4ac38b1.png)

