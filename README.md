# Weighted-Class-Tfidf
[![forthebadge made-with-python](http://ForTheBadge.com/images/badges/made-with-python.svg)](https://www.python.org/)[![ForTheBadgebuilt-with-love](http://ForTheBadge.com/images/badges/built-with-love.svg)](https://github.com/SauravPattnaikCS60/Weighted-Class-Based-Tfidf)

## Inspiration behind WCBTFIDF

Standard tfidf models select the features(number defined by the **max_features** param) using t**erm frequency** alone.
This can create problems when the dataset is imbalanced resulting in words from the majority class being selected.
As a result of this minority class gets under-represented in the matrix that is being returned by tfidf.


## Solution

To tackle this problem we break down the tfidf process class wise.
Let us consider an example to understand what WCBTFIDF does under the hood

Assume a dataset having two labels 0 and 1.
**0** is present in **80%** of the records and **1** is present in **20%** of the records.

If we run standard tfidf on this(with for example 300 features) it will pick the top 300 words by frequency
from both the classes. There is a very high chance that words selected will be majorly from class 0 and we 
might run the risk of under-representing class 1 severely.

What wcbtfidf does is that first it calculates weight for each label.
Weight here refers to how many features it should select from each class.

Since class 0 is present in 80% of the records, wcbtfidf will pick 240 features from class 0 and 60 features
from class 1.

So essentially we run tfidf class wise on 0 and 1 labels with max features set as 240 and 60.

After doing that, we combine the vocabulary from both these classes into a single list.It can be easily done since
tfidf provides a **vocabulary_** param that stores the vocab.

Finally this combined vocab is used as a fixed vocabulary in another tfidf model that is ran on the entire data.
By fixing the vocab for the final tfidf we ensure that we are going to score on these set of words only.

_To put it simply the 300 features choosen by wcbtfidf are a better representation of the overall data as compared
to the features chosen by standard tfidf model._

## RESULTS

In the experiments conducted, wcbtfidf performed better than standard tfidf models. The results have been put
into a notebook under the _demos_ folder.

