---
layout: docs
header: true
layout: article
title: NLU release notes
permalink: /docs/en/release_notes
key: docs-release-notes
modify_date: "2020-06-12"
---

<div class="main-docs" markdown="1">


<div class="h3-box" markdown="1">

component_examples/

## NLU 1.1.0 Release Notes 
We are incredibly happy to announce NLU 1.1.0 is released and it integrates the X models in
Y languages of the new Spark-NLP 2.7.0 release.
You can now summarize text, answer questions, translate between 300 languages and mine various
amount of multi-lingual data.

### New Notebooks, Tutorials and Articles
- Translate between 300 languages with marian
- Try out the 17 Tasks on T5
- Tokenize chinese and classify NER
- Tokenize chinese and Korean NER
- Tokenize chinese and Japanese NER

- Aspect based NER
=   Pre-Trained tokenizers for THai, Japanese, Korean and Chinese





##  NLU 1.0.6 Release Notes
### Trainable Multi Label Classifiers, predict Stackoverflow Tags and much more in 1 Line of with NLU 1.0.6
We are glad to announce NLU 1.0.6 has been released!
NLU 1.0.6 comes with the Multi Label classifier, it can learn to map strings to multiple labels.
The Multi Label Classifier is using Bidirectional GRU and CNNs inside TensorFlow and supports up to 100 classes.

### NLU 1.0.6 New Features
- Multi Label Classifier
   - The Multi Label Classifier learns a 1 to many mapping between text and labels. This means it can predict multiple labels at the same time for a given input string. This is very helpful for tasks similar to content tag prediction (HashTags/RedditTags/YoutubeTags/Toxic/E2e etc..)
   - Support up to 100 classes
   - Pre-trained Multi Label Classifiers are already avaiable as [Toxic](https://nlu.johnsnowlabs.com/docs/en/examples#toxic-classifier) and [E2E](https://nlu.johnsnowlabs.com/docs/en/examples#e2e-classifier) classifiers

####  Multi Label Classifier
- [ Train Multi Label Classifier on E2E dataset Demo](https://colab.research.google.com/drive/15ZqfNUqliRKP4UgaFcRg5KOSTkqrtDXy?usp=sharing)
- [Train Multi Label  Classifier on Stack Overflow Question Tags dataset Demo](https://colab.research.google.com/drive/1Y0pYdUMKSs1ZP0NDcKgVECqkKD9ShIdc?usp=sharing)       
  This model can predict multiple labels for one sentence.
  To train the Multi Label text classifier model, you must pass a dataframe with a ```text``` column and a ```y``` column for the label.   
  The ```y``` label must be a string column where each label is seperated with a seperator.     
  By default, ```,``` is assumed as line seperator.      
  If your dataset is using a different label seperator, you must configure the ```label_seperator``` parameter while calling the ```fit()``` method.

By default *Universal Sentence Encoder Embeddings (USE)* are used as sentence embeddings for training.

```python
fitted_pipe = nlu.load('train.multi_classifier').fit(train_df)
preds = fitted_pipe.predict(train_df)
```

If you add a nlu sentence embeddings reference, before the train reference, NLU will use that Sentence embeddings instead of the default USE.
```python
#Train on BERT sentence emebddings
fitted_pipe = nlu.load('embed_sentence.bert train.multi_classifier').fit(train_df)
preds = fitted_pipe.predict(train_df)
```

Configure a custom line seperator
```python
#Use ; as label seperator
fitted_pipe = nlu.load('embed_sentence.electra train.multi_classifier').fit(train_df, label_seperator=';')
preds = fitted_pipe.predict(train_df)
```


### NLU 1.0.6 Enhancements
- Improved outputs for Toxic and E2E Classifier.
  - by default, all predicted classes and their confidences which are above the threshold will be returned inside of a list in the Pandas dataframe
  - by configuring meta=True, the confidences for all classes will be returned.


### NLU 1.0.6 New Notebooks and Tutorials

- [ Train Multi Label Classifier on E2E dataset](https://colab.research.google.com/drive/15ZqfNUqliRKP4UgaFcRg5KOSTkqrtDXy?usp=sharing)
- [Train Multi Label  Classifier on Stack Overflow Question Tags dataset](https://drive.google.com/file/d/1Nmrncn-y559od3AKJglwfJ0VmZKjtMAF/view?usp=sharing)

### NLU 1.0.6 Bug-fixes
- Fixed a bug that caused ```en.ner.dl.bert``` to be inaccessible
- Fixed a bug that caused ```pt.ner.large``` to be inaccessible
- Fixed a bug that caused USE embeddings not properly beeing configured to document level output when using multiple embeddings at the same time


##  NLU 1.0.5 Release Notes 

### Trainable Part of Speech Tagger (POS), Sentiment Classifier with BERT/USE/ELECTRA sentence embeddings in 1 Line of code! Latest NLU Release 1.0.5
We are glad to announce NLU 1.0.5 has been released!       
This release comes with a **trainable Sentiment classifier** and a **Trainable Part of Speech (POS)** models!       
These Neural Network Architectures achieve the state of the art (SOTA) on most **binary Sentiment analysis** and **Part of Speech Tagging** tasks!       
You can train the Sentiment Model on any of the **100+ Sentence Embeddings** which include **BERT, ELECTRA, USE, Multi Lingual BERT Sentence Embeddings** and many more!       
Leverage this and achieve the state of the art in any of your datasets, all of this in **just 1 line of Python code**

### NLU 1.0.5 New Features
- Trainable Sentiment DL classifier
- Trainable POS

### NLU 1.0.5 New Notebooks and Tutorials 
- [Sentiment Classification Training Demo](https://colab.research.google.com/drive/1f-EORjO3IpvwRAktuL4EvZPqPr2IZ_g8?usp=sharing)
- [Part Of Speech Tagger Training demo](https://colab.research.google.com/drive/1CZqHQmrxkDf7y3rQHVjO-97tCnpUXu_3?usp=sharing)

### Sentiment Classifier Training
[Sentiment Classification Training Demo](https://colab.research.google.com/drive/1f-EORjO3IpvwRAktuL4EvZPqPr2IZ_g8?usp=sharing)

To train the Binary Sentiment classifier model, you must pass a dataframe with a 'text' column and a 'y' column for the label.

By default *Universal Sentence Encoder Embeddings (USE)* are used as sentence embeddings.

```python
fitted_pipe = nlu.load('train.sentiment').fit(train_df)
preds = fitted_pipe.predict(train_df)
```

If you add a nlu sentence embeddings reference, before the train reference, NLU will use that Sentence embeddings instead of the default USE.

```python
#Train Classifier on BERT sentence embeddings
fitted_pipe = nlu.load('embed_sentence.bert train.classifier').fit(train_df)
preds = fitted_pipe.predict(train_df)
```

```python
#Train Classifier on ELECTRA sentence embeddings
fitted_pipe = nlu.load('embed_sentence.electra train.classifier').fit(train_df)
preds = fitted_pipe.predict(train_df)
```

### Part Of Speech Tagger Training 
[Part Of Speech Tagger Training demo](https://colab.research.google.com/drive/1CZqHQmrxkDf7y3rQHVjO-97tCnpUXu_3?usp=sharing)

```python
fitted_pipe = nlu.load('train.pos').fit(train_df)
preds = fitted_pipe.predict(train_df)
```



### NLU 1.0.5 Installation changes
Starting from version 1.0.5 NLU will not automatically install pyspark for users anymore.      
This enables easier customizing the Pyspark version which makes it easier to use in various cluster enviroments.

To install NLU from now on, please run
```bash
pip install nlu pyspark==2.4.7 
```
or install any pyspark>=2.4.0 with pyspark<3

### NLU 1.0.5 Improvements
- Improved Databricks path handling for loading and storing models.




## NLU  1.0.4 Release Notes 
##  John Snow Labs NLU 1.0.4 : Trainable Named Entity Recognizer (NER) , achieve SOTA in 1 line of code and easy scaling to 100's of Spark nodes
We are glad to announce NLU 1.0.4 releases the State of the Art breaking Neural Network architecture for NER, Char CNNs - BiLSTM - CRF!

```python
#fit and predict in 1 line!
nlu.load('train.ner').fit(dataset).predict(dataset)


#fit and predict in 1 line with BERT!
nlu.load('bert train.ner').fit(dataset).predict(dataset)


#fit and predict in 1 line with ALBERT!
nlu.load('albert train.ner').fit(dataset).predict(dataset)


#fit and predict in 1 line with ELMO!
nlu.load('elmo train.ner').fit(dataset).predict(dataset)

```



Any NLU pipeline stored can now be loaded as pyspark ML pipeline
```python
# Ready for big Data with Spark distributed computing
import pyspark
nlu_pipe.save(path)
pyspark_pipe = pyspark.ml.PipelineModel.load(stored_model_path)
pyspark_pipe.transform(spark_df)
```


### NLU 1.0.4 New Features
- Trainable  [Named Entity Recognizer](https://nlp.johnsnowlabs.com/docs/en/annotators#ner-dl-named-entity-recognition-deep-learning-annotator)
- NLU pipeline loadable as Spark pipelines

### NLU 1.0.4 New Notebooks,Tutorials and Docs
- [NER training demo](https://colab.research.google.com/drive/1_GwhdXULq45GZkw3157fAOx4Wqo-fmFV?usp=sharing)        
- [Multi Class Text Classifier Training Demo updated to showcase usage of different Embeddings](https://colab.research.google.com/drive/12FA2TVvvRWw4pRhxDnK32WAzl9dbF6Qw?usp=sharing)         
- [New Documentation Page on how to train Models with NLU](https://nlu.johnsnowlabs.com/docs/en/training)
- Databricks Notebook showcasing Scaling with NLU


## NLU 1.0.4 Bug Fixes
- Fixed a bug that NER token confidences do not appear. They now appear when nlu.load('ner').predict(df, meta=True) is called.
- Fixed a bug that caused some Spark NLP models to not be loaded properly in offline mode



## 1.0.3 Release Notes 
We are happy to announce NLU 1.0.3 comes with a lot new features, training classifiers, saving them and loading them offline, enabling running NLU with no internet connection, new notebooks and articles!

### NLU 1.0.3 New Features
- Train a Deep Learning classifier in 1 line! The popular [ClassifierDL](https://nlp.johnsnowlabs.com/docs/en/annotators#classifierdl-multi-class-text-classification)
which can achieve state of the art results on any multi class text classification problem is now trainable!
All it takes is just nlu.load('train.classifier).fit(dataset) . Your dataset can be a Pandas/Spark/Modin/Ray/Dask dataframe and needs to have a column named x for text data and a column named y for labels
- Saving pipelines to HDD is now possible with nlu.save(path)
- Loading pipelines from disk now possible with nlu.load(path=path). 
- NLU offline mode: Loading from disk makes running NLU offline now possible, since you can load pipelines/models from your local hard drive instead of John Snow Labs AWS servers.

### NLU 1.0.3 New Notebooks and Tutorials
- New colab notebook showcasing nlu training, saving and loading from disk
- [Sentence Similarity with BERT, Electra and Universal Sentence Encoder Medium Tutorial](https://medium.com/spark-nlp/easy-sentence-similarity-with-bert-sentence-embeddings-using-john-snow-labs-nlu-ea078deb6ebf)
- [Sentence Similarity with BERT, Electra and Universal Sentence Encoder](https://colab.research.google.com/drive/1LtOdtXtRJ3_N8kYywPd5k2AJMCGcgAdN?usp=sharing)
- [Train a Deep Learning Classifier ](https://colab.research.google.com/drive/12FA2TVvvRWw4pRhxDnK32WAzl9dbF6Qw?usp=sharing)
- [Sentence Detector Notebook Updated](https://colab.research.google.com/drive/1CAXEdRk_q3U5qbMXsxoVyZRwvonKthhF?usp=sharing)
- [New Workshop video](https://events.johnsnowlabs.com/cs/c/?cta_guid=8b2b188b-92a3-48ba-ad7e-073b384425b0&signature=AAH58kFAHrVT-HfvWFxdTg_lm8reKUdTBw&pageId=25538044150&placement_guid=c659363c-2188-4c86-945f-5cfb7b42fcfc&click=8cd42d22-2f03-4358-a9e8-0d8f9aa33139&hsutk=c7a000001cda197314f90175e307161f&canon=https%3A%2F%2Fevents.johnsnowlabs.com%2Fwebinars&utm_referrer=https%3A%2F%2Fwww.johnsnowlabs.com%2F&portal_id=1794529&redirect_url=APefjpGh4Q9Hy0Mg9Ezy0_kJOOLC3l5QYyJsCSfZc1Lf61qrn2Bk6OQIJj65atZ9zzzrNrxuDPk5EHt94G0ZcIJaP_QMuD_E7fnMeJs4bQrEdLl7HE2MC4WNHGB6t1cqABfjZntS_TYSaj02yJNDf6p7Zaj9OYy0qQCmM8bbeuVgxUe6s5946UqHDsVHrpY0Oa2Fs7DJXIahZsB08hGkVj3qSHIM5vpjsA)


### NLU 1.0.3 Bug fixes
- Sentence Detector bugfix 




## NLU 1.0.2 Release Notes 

We are glad to announce nlu 1.0.2 is released!

### NLU 1.0.2  Enhancements
- More semantically concise output levels sentence and document enforced : 
  - If a pipe is set to output_level='document' : 
    -  Every Sentence Embedding will generate 1 Embedding per Document/row in the input Dataframe, instead of 1 embedding per sentence. 
    - Every  Classifier will classify an entire Document/row 
    - Each row in the output DF is a 1 to 1 mapping of the original input DF. 1 to 1 mapping from input to output.
  - If a pipe is set to output_level='sentence' : 
    -  Every Sentence Embedding will generate 1 Embedding per Sentence, 
    - Every  Classifier will classify exactly one sentence
    - Each row in the output DF can is mapped to one row in the input DF, but one row in the input DF can have multiple corresponding rows in the output DF. 1 to N mapping from input to output.
- Improved generation of column names for classifiers. based on input nlu reference
- Improved generation of column names for embeddings, based on input nlu reference
- Improved automatic output level inference
- Various test updates
- Integration of CI pipeline with Github Actions 

### New  Documentation is out!
Check it out here :  http://nlu.johnsnowlabs.com/


## NLU 1.0.1 Release Notes 

### NLU 1.0.1 Bugfixes
- Fixed bug that caused NER pipelines to crash in NLU when input string caused the NER model to predict without additional metadata

## 1.0 Release Notes 
- Automatic to Numpy conversion of embeddings
- Added various testing classes
- [New 6 embeddings at once notebook with t-SNE and Medium article](https://medium.com/spark-nlp/1-line-of-code-for-bert-albert-elmo-electra-xlnet-glove-part-of-speech-with-nlu-and-t-sne-9ebcd5379cd)
 <img src="https://miro.medium.com/max/1296/1*WI4AJ78hwPpT_2SqpRpolA.png" >
- Integration of Spark NLP 2.6.2 enhancements and bugfixes https://github.com/JohnSnowLabs/spark-nlp/releases/tag/2.6.2
- Updated old T-SNE notebooks with more elegant and simpler generation of t-SNE embeddings 

</div><div class="h3-box" markdown="1">

## 0.2.1 Release Notes 
- Various bugfixes
- Improved output column names when using multiple classifirs at once

</div><div class="h3-box" markdown="1">

## 0.2 Release Notes 
-   Improved output column names  classifiers

</div><div class="h3-box" markdown="1">
    
## 0.1 Release Notes



# 1.0 Release Notes 
- Automatic to Numpy conversion of embeddings
- Added various testing classes
- [New 6 embeddings at once notebook with t-SNE and Medium article](https://medium.com/spark-nlp/1-line-of-code-for-bert-albert-elmo-electra-xlnet-glove-part-of-speech-with-nlu-and-t-sne-9ebcd5379cd)
 <img src="https://miro.medium.com/max/1296/1*WI4AJ78hwPpT_2SqpRpolA.png" >
- Integration of Spark NLP 2.6.2 enhancements and bugfixes https://github.com/JohnSnowLabs/spark-nlp/releases/tag/2.6.2
- Updated old T-SNE notebooks with more elegant and simpler generation of t-SNE embeddings 

# 0.2.1 Release Notes 
- Various bugfixes
- Improved output column names when using multiple classifirs at once

# 0.2 Release Notes 
-   Improved output column names  classifiers
    
# 0.1 Release Notes
We are glad to announce that NLU 0.0.1 has been released!
NLU makes the 350+ models and annotators in Spark NLPs arsenal available in just 1 line of python code and it works with Pandas dataframes!
A picture says more than a 1000 words, so here is a demo clip of the 12 coolest features in NLU, all just in 1 line!

</div><div class="h3-box" markdown="1">

## NLU in action 
<img src="http://ckl-it.de/wp-content/uploads/2020/08/My-Video6.gif" width="1800" height="500"/>

</div><div class="h3-box" markdown="1">

## What does NLU 0.1 include?

## NLU in action 
<img src="http://ckl-it.de/wp-content/uploads/2020/08/My-Video6.gif" width="1800" height="500"/>

# What does NLU 0.1 include?
 - NLU provides everything a data scientist might want to wish for in one line of code!
 - 350 + pre-trained models
 - 100+ of the latest NLP word embeddings ( BERT, ELMO, ALBERT, XLNET, GLOVE, BIOBERT, ELECTRA, COVIDBERT) and different variations of them
 - 50+ of the latest NLP sentence embeddings ( BERT, ELECTRA, USE) and different variations of them
 - 50+ Classifiers (NER, POS, Emotion, Sarcasm, Questions, Spam)
 - 40+ Supported Languages
 - Labeled and Unlabeled Dependency parsing
 - Various Text Cleaning and Pre-Processing methods like Stemming, Lemmatizing, Normalizing, Filtering, Cleaning pipelines and more

 </div><div class="h3-box" markdown="1">

## NLU 0.1 Features Google Collab Notebook Demos

- Named Entity Recognition (NER)
    - [NER pretrained on ONTO Notes](https://colab.research.google.com/drive/1_sgbJV3dYPZ_Q7acCgKWgqZkWcKAfg79?usp=sharing)
    - [NER pretrained on CONLL](https://colab.research.google.com/drive/1CYzHfQyFCdvIOVO2Z5aggVI9c0hDEOrw?usp=sharing)
</div><div class="h3-box" markdown="1">

- Part of speech (POS)
    - [POS pretrained on ANC dataset](https://colab.research.google.com/drive/1tW833T3HS8F5Lvn6LgeDd5LW5226syKN?usp=sharing)

</div><div class="h3-box" markdown="1">

# NLU 0.1 Features Google Collab Notebook Demos

- Named Entity Recognition (NER)
    -[NER pretrained on ONTO Notes](https://colab.research.google.com/drive/1_sgbJV3dYPZ_Q7acCgKWgqZkWcKAfg79?usp=sharing)
    -[NER pretrained on CONLL](https://colab.research.google.com/drive/1CYzHfQyFCdvIOVO2Z5aggVI9c0hDEOrw?usp=sharing)
- Part of speech (POS)
    - [POS pretrained on ANC dataset](https://colab.research.google.com/drive/1tW833T3HS8F5Lvn6LgeDd5LW5226syKN?usp=sharing)
- Classifiers
    - [Unsupervised Keyword Extraction with YAKE](https://colab.research.google.com/drive/1BdomIc1nhrGxLFOpK5r82Zc4eFgnIgaO?usp=sharing)
    - [Toxic Text Classifier](https://colab.research.google.com/drive/1QRG5ZtAvoJAMZ8ytFMfXj_W8ogdeRi9m?usp=sharing)
    - [Twitter Sentiment Classifier](https://colab.research.google.com/drive/1H1Gekn2qzXzOf5rrT8LmHmmuoOGsiu8m?usp=sharing)
    - [Movie Review Sentiment Classifier](https://colab.research.google.com/drive/1k5x1zxnG4bBkmYAc-bc63sMA4-oQ6-dP?usp=sharing)
    - [Sarcasm Classifier](https://colab.research.google.com/drive/1XffsjlRp9wxZgxyYvEF9bG2CiX-pjBEw?usp=sharing)
    - [50 Class Questions Classifier](https://colab.research.google.com/drive/1OwlmLzwkcJKhuz__RUH74O9HqFZutxzS?usp=sharing)
    - [20 Class Languages Classifier](https://colab.research.google.com/drive/1CzMfRFJZsj4j1fhormDQdHOIV5IybC57?usp=sharing)
    - [Fake News Classifier](https://colab.research.google.com/drive/1QuoeGLgmtkUnDQQ2oVS1tuZC2qHDj3p9?usp=sharing)
    - [E2E Classifier](https://colab.research.google.com/drive/1OSkiXGEpKlm9HWDoVb42uLNQQgb7nqNZ?usp=sharing)
    - [Cyberbullying Classifier](https://colab.research.google.com/drive/1OSkiXGEpKlm9HWDoVb42uLNQQgb7nqNZ?usp=sharing)
    - [Spam Classifier](https://colab.research.google.com/drive/1u-8Fs3Etz07bFNx0CDV_le3Xz73VbK0z?usp=sharing)

</div><div class="h3-box" markdown="1">

- Word and Sentence Embeddings 
    - [BERT Word Embeddings and T-SNE plotting](https://colab.research.google.com/drive/1Rg1vdSeq6sURc48RV8lpS47ja0bYwQmt?usp=sharing)
    - [BERT Sentence Embeddings and T-SNE plotting](https://colab.research.google.com/drive/1FmREx0O4BDeogldyN74_7Lur5NeiOVye?usp=sharing)
    - [ALBERT Word Embeddings and T-SNE plotting](https://colab.research.google.com/drive/18yd9pDoPkde79boTbAC8Xd03ROKisPsn?usp=sharing)
    - [ELMO Word Embeddings and T-SNE plotting](https://colab.research.google.com/drive/1TtNYB9z0yH8d1ZjfxkH0TVxQ2O_iOYVV?usp=sharing)
    - [XLNET Word Embeddings and T-SNE plotting](https://colab.research.google.com/drive/1C9T29QA00yjLuJ1yEMTbjUQMpUv35pHb?usp=sharing)
    - [ELECTRA Word Embeddings and T-SNE plotting](https://colab.research.google.com/drive/1FueGEaOj2JkbqHzdmxwKrNMHzgVt4baE?usp=sharing)
    - [COVIDBERT Word Embeddings and T-SNE plotting](https://colab.research.google.com/drive/1Yzc-GuNQyeWewJh5USTN7PbbcJvd-D7s?usp=sharing)
    - [BIOBERT Word Embeddings and T-SNE plotting](https://colab.research.google.com/drive/1llANd-XGD8vkGNMcqTi_8Dr_Ys6cr83W?usp=sharing)
    - [GLOVE Word Embeddings and T-SNE plotting](https://colab.research.google.com/drive/1IQxf4pJ_EnrIDyd0fAX-dv6u0YQWae2g?usp=sharing)
    - [USE Sentence Embeddings and T-SNE plotting](https://colab.research.google.com/drive/1gZzOMiCovmrp7z8FIidzDTLS0nt8kPJT?usp=sharing)

</div><div class="h3-box" markdown="1">

- Depenency Parsing 
    - [Untyped Dependency Parsing](https://colab.research.google.com/drive/1PC8ga_NFlOcTNeDVJY4x8Pl5oe0jVmue?usp=sharing)
    - [Typed Dependency Parsing](https://colab.research.google.com/drive/1KXUqcF8e-LU9cXnHE8ni8z758LuFPvY7?usp=sharing)

</div><div class="h3-box" markdown="1">

- Depenency Parsing 
    -[Untyped Dependency Parsing](https://colab.research.google.com/drive/1PC8ga_NFlOcTNeDVJY4x8Pl5oe0jVmue?usp=sharing)
    -[Typed Dependency Parsing](https://colab.research.google.com/drive/1KXUqcF8e-LU9cXnHE8ni8z758LuFPvY7?usp=sharing)

- Text Pre Processing and Cleaning
    - [Tokenization](https://colab.research.google.com/drive/13BC6k6gLj1w5RZ0SyHjKsT2EOwJwbYwb?usp=sharing)
    - [Stopwords removal](https://colab.research.google.com/drive/1nWob4u93t2EJYupcOIanuPBDfShtYjGT?usp=sharing)
    - [Stemming](https://colab.research.google.com/drive/1gKTJJmffR9wz13Ms3pDy64jhUI8ZHZYu?usp=sharing)
    - [Lemmatization](https://colab.research.google.com/drive/1cBtx9cVCjavt-Oq5TG1lO-9JfUfqznnK?usp=sharing)
    - [Normalizing](https://colab.research.google.com/drive/1kfnnwkiQPQa465Jic6va9QXTRssU4mlX?usp=sharing)
    - [Spellchecking](https://colab.research.google.com/drive/1bnRR8FygiiN3zJz3mRdbjPBUvFsx6IVB?usp=sharing)
    - [Sentence Detecting](https://colab.research.google.com/drive/1CAXEdRk_q3U5qbMXsxoVyZRwvonKthhF?usp=sharing)

</div><div class="h3-box" markdown="1">

- Chunkers
    - [N Gram](https://colab.research.google.com/drive/1pgqoRJ6yGWbTLWdLnRvwG5DLSU3rxuMq?usp=sharing)
    - [Entity Chunking](https://colab.research.google.com/drive/1svpqtC3cY6JnRGeJngIPl2raqxdowpyi?usp=sharing)

</div><div class="h3-box" markdown="1">

- Matchers
    - [Date Matcher](https://colab.research.google.com/drive/1JrlfuV2jNGTdOXvaWIoHTSf6BscDMkN7?usp=sharing)

</div><div class="h3-box" markdown="1">


</div></div>
- Chunkers
    -[N Gram](https://colab.research.google.com/drive/1pgqoRJ6yGWbTLWdLnRvwG5DLSU3rxuMq?usp=sharing)
    -[Entity Chunking](https://colab.research.google.com/drive/1svpqtC3cY6JnRGeJngIPl2raqxdowpyi?usp=sharing)
- Matchers
    -[Date Matcher](https://colab.research.google.com/drive/1JrlfuV2jNGTdOXvaWIoHTSf6BscDMkN7?usp=sharing)




