---
layout: post
title: Detecting Machine Translation
---
### __TL;DR__
 I and Ricardo Martins decided to participate on the JEEC/Unbabel Machine Translation Detection Challenge, we ended in 4th place. The Code and dataset are available on the project [Github](https://github.com/Joao-M-Almeida/JEECUnbabelChallenge).

### The Challenge


At the [JEEC16](http://jeec.tecnico.pt/jeec16/) (a Electrical and Computer Engineering event organized by the students at [Técnico](http://tecnico.ulisboa.pt)) conference [Unbabel](https://unbabel.com/) (a Portuguese startup that does human powered machine translation) went to give a talk and proposed a challenge to the students attending. I and Ricardo Martins decided to participate.

The __goal__ of the challenge was, given a dataset of spanish phrases, to create a model that would __distinguish between human and machine translations__.

### The Data

The available dataset consisted of about [20K labeled phrases](https://github.com/Joao-M-Almeida/JEECUnbabelChallenge/blob/master/Data/OficialData/training.txt). And the final test set of [3220 phrases to classify](https://github.com/Joao-M-Almeida/JEECUnbabelChallenge/blob/master/Data/OficialData/test_blind.txt).

These data consisted of phrases translated by machines (label: 0) or by humans (label: 1). We didn't know where this data had been acquired, however by examining it we suspected it was from online news stories.

### What we tried

#### The basics
Despite our interest on Machine learning we didn't have any experience on natural language processing. So, we started from the basics.

We used [NLTK](nltk.org) and [scikit-learn](http://scikit-learn.org/) to:

- Transform the text into a bag-of-words (BoW);
- N-grams representation;
- Lemmatization and Stemming;
- Multiple classifiers from scikit-learn, evaluated with cross validation and tuned with Grid Search;

Then we tried to spice things up by testing:

- Part-of-Speech (POS) Tagging;
- Manualy Crafting features;
- Adding external data;

#### Bag-of-Words

With the [TfIdfVectorizer from scikit-learn](http://scikit-learn.org/stable/modules/generated/sklearn.feature_extraction.text.TfidfVectorizer.html) we created a vector representation of the textual data.

On the BoW data we applied the TruncatedSVD method with 200 components to reduce it's dimensionality.

#### POS Tagged Bi-grams

To have a more rich representation of the textual data we transformed it into bi-grams and run the [Stanford POS Tagger](http://nlp.stanford.edu/software/tagger.shtml) . These features ended up giving the largest boost to our accuracy.

#### Handmade Features

We wondered if there were common spanish mistakes made by the machine translator. With this idea in mind we implemented sole hand made features, from [this list](http://community.languagetool.org/rule/list?lang=es), to try to help our system detect common errors on machine translations.
This ended improving our cross validated score on about 1%.

#### Getting more data
As 20K samples is a small dataset for Natural Language Tasks we searched for some external data that could aid our efforts. Since we didn't find any dataset for this task we decided to create one from [The Billingual News](http://www.thebilingualnews.com/) and with the help of [Google Translate](http://translate.google.com/). This was done manualy and the resulting dataset was of poor quality so we ended up giving up. We were running out of time and our results weren't improving with this extra data.

### What worked best

A Voting Classifier based on LDA, LogisticRegression and AdaBoost with on the handmade features and on the POS Tagged bi-grams with dimensionality reduction by pricinpal component analysis.

### Interesting discovery

One of the most intriguing results we got was when applying KNN classifiers (K = 3 or 5 ) to the problem. The __cross validadted accuracy was of about 30%__ which is a weird value for a binary classification task. This means we would be __substancially better off chosing exactly the oposite of the predicted label__.

This result is even more stunning if we take into account that the best performing classifiers were achieving about 55%.

 _How could this model have such a low accuracy?_

We understood what happened when we noticed that in the given dataset some of the same phrases were translated by humans and by machines. This meant that our KNN approach were finding on the test set the complementary phrase to the one it had been trained on. This led the algorithm to predict those labels incorrectly.

This situation could have been explored (we could achieve about 70% cross validaded accuracy), however we decided not to do it for two main reasons:

1. Creating a model based on this artifact didn't seem correct, we would only have good results on this dataset and not on real world data.
2. There was a chance that the test dataset could not have any of the complementary phrases to the ones on the dataset, which would mean much worse results.

### Final Results:
 Our final model achieved a cross validation score of (55.0 +/- 1.6)% and a final result of 57.8%.

#### Global Results:
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
