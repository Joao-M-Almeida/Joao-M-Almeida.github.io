---
layout: post
title: Detecting Machine Translation
---
## __TL;DR__
 I and Ricardo Martins decided to participate on the JEEC/Unbabel Machine Translation Detection Challenge, we ended in 4th place. The Code and dataset are available on the project [Github](https://github.com/Joao-M-Almeida/JEECUnbabelChallenge).

## The Challenge


At the [JEEC16](http://jeec.tecnico.pt/jeec16/) (a Electrical and Computer Engineering event organized by the students at [Técnico](http://tecnico.ulisboa.pt)) conference [Unbabel](https://unbabel.com/) (a Portuguese startup that does human powered machine translation) went to give a talk and proposed a challenge to the students attending. I and Ricardo Martins decided to participate.

The __goal__ of the challenge was, given a dataset of spanish phrases, to create a model that would __distinguish between human and machine translations__.

## The Data

The available dataset consisted of about [20K labeled phrases](https://github.com/Joao-M-Almeida/JEECUnbabelChallenge/blob/master/Data/OficialData/training.txt) either translated by machines (label: 0) or by humans (label: 1). And the final test set of [3220 phrases to classify](https://github.com/Joao-M-Almeida/JEECUnbabelChallenge/blob/master/Data/OficialData/test_blind.txt).

We didn't know where this data had been acquired, however by examining it we suspected it was from online news stories.

## What we tried

### The basics
Despite our interest on Machine learning we didn't have any experience on natural language processing. So, we started from the basics. We tried:

- Transforming the text into a bag-of-words (BoW);
- N-grams representation;
- Lemmatization and Stemming;
- Multiple classifiers from [scikit-learn](http://scikit-learn.org), evaluated with cross validation and tuned with Grid Search;

Then we tried to spice things up by testing:

- Part-of-Speech (POS) Tagging;
- Manualy Crafting features;
- Adding external data;

### Bag-of-Words

With the [TfIdfVectorizer from scikit-learn](http://scikit-learn.org/stable/modules/generated/sklearn.feature_extraction.text.TfidfVectorizer.html) we created a vector representation of the textual data.

On the BoW data we applied the TruncatedSVD method with 200 components to reduce it's dimensionality.

### POS Tagged Bi-grams

To have a more rich representation of the textual data we transformed it into bi-grams and run the [Stanford POS Tagger](http://nlp.stanford.edu/software/tagger.shtml) . These features ended up giving the __largest boost to our accuracy__.

### Handmade Features

We wondered if there were __common spanish mistakes__ made by the machine translator. With this idea in mind we implemented some hand made features, from [this list](http://community.languagetool.org/rule/list?lang=es), to try to help our system detect common errors on machine translations.
This ended __improving our cross validated score on about 1%__.

### Getting more data
As 20K samples is a small dataset for Natural Language Tasks we searched for some external data that could aid our efforts. Since we didn't find any dataset for this task we decided to create one from [The Billingual News](http://www.thebilingualnews.com/) with the help of [Google Translate](http://translate.google.com/). This was done manualy and the resulting dataset was of poor quality so we ended up giving up. We were running out of time and our results weren't improving with this extra data.

## What worked best

A __Voting Classifier__ based on __LDA__, __LogisticRegression__ and __AdaBoost__ with on the __handmade features__ and on the __POS Tagged bi-grams__ with dimensionality reduction by __pricinpal component analysis__.

## An Interesting discovery

One of the most intriguing results we got was when applying KNN classifiers (K = 3 or 5 ) to the problem. The __cross validadted accuracy was of about 30%__ which is a weird value for a binary classification task. This means we would be __substancially better off chosing exactly the oposite of the predicted label__.

This result is even more stunning if we take into account that the best performing classifiers were achieving about 55%.

 **_How could this model have such a low accuracy?_**

We understood what happened when we noticed that in the given dataset some of the same phrases were translated by humans and by machines. This meant that our KNN approach were finding on the test set the complementary phrase to the one it had been trained on. This led the algorithm to predict those labels incorrectly.

This situation could have been explored (we could achieve about __70% cross validaded accuracy__), however we decided not to do it for __two__ main reasons:

1. Creating a model based on this artifact __didn't seem correct__, we would only have good results on this dataset and not on real world data.
2. There was a chance that the test dataset could not have any of the complementary phrases to the ones on the dataset, which __would mean much worse results__.

## Final Results:
 Our final model achieved a __cross validation score of (55.0 +/- 1.6)%__ and a __final result of 57.8%__.

### Global Results:
1. Francisco Dias: 59.72%
2. Catarina Silva: 59.22%
3. Miguel Borges Ribeiro, Tiago Baltazar: 58.39%
4. __João Almeida, Ricardo Martins: 57.80%__
5. João Rocha e Melo, Miguel Monteiro: 56.34%
6. António Lopes: 55.62%
7. Tiago Santos, Nuno Xu: 51.77%
8. Bruno Henriques, Joana Lapas: 50.25%
9. Sandro Nunes: 47.86%
10. Gonçalo Correia: 47.61%
11. Ricardo Amendoeira: 45.56%
12. Jorge Matos: 40.43%
13. Luis Novoa, Maria Carvalho: 0.00% (file missing results)
