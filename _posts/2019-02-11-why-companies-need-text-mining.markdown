---
layout: single
title:  "Why companies need text mining"
date:   2018-02-11 16:00:00 +0100
categories: analytics
header:
    overlay_image: /assets/images/old-docs.jpeg
    show_overlay_excerpt: false
    overlay_filter: rgba(0, 73, 101, 0.5)
    teaser: /assets/images/old-docs-teaser.jpeg
---

The business world is littered with all kinds of documents which contain important data. Corporate employees have to process thousands of documents every day. Ranging from various contracts, reports, documentation to spreadsheets and receipts. Manual entry into enterprise systems is a tedious and error prone process that does not ensure that the data input really reflects what is in the document.

Let's explore some typical challenges and some basic starting steps, tools and methodologies that will help companies to handle their document processing tasks.

## Storage, Digitalization and Records Management

Many companies still process and store a lot of paper documents. These take up a lot of space and need to be stored in specific ways for easy retrieval if needed. It is very difficult and expensive to set this up, so more and more companies invest in scanning and store the digital scans in [Enterprise Content Management (ECM)](https://en.wikipedia.org/wiki/Enterprise_content_management) systems.
To turn these scans (which are images) into searchable plain text format an [Optical Character Recognition (OCR)](https://en.wikipedia.org/wiki/Optical_character_recognition) tool is required.

A global company must be able to handle documents in many languages. Languages like Arabic and Chinese are difficult to process and the company needs to make sure that all the enterprise systems can work with these languages.
[Unicode standard](https://en.wikipedia.org/wiki/Unicode) should be preferred.

Having a [Records Management](https://en.wikipedia.org/wiki/Records_management) function supported by enterprise systems is very beneficial. Proper RM can help reducing document processing workloads and also helps to filter out the documents that are no longer relevant to the business. 

Starting points:
- [Optical Character Recognition (OCR)](https://en.wikipedia.org/wiki/Optical_character_recognition) - to convert scans into plain text
- [Enterprise Content Management (ECM)](https://en.wikipedia.org/wiki/Enterprise_content_management) - to store documents and metadata
- [Unicode](https://en.wikipedia.org/wiki/Unicode) - to ensure consistent document encoding
- [Records Management](https://en.wikipedia.org/wiki/Records_management) - to manage lifecycle of information


## Searching

Reading a 100 page contract to answer a simple question consumes a lot of time. Searching the text for a specific term might lead to the desired information but often it is hard to know the exact phrase to search for. The document might be written in such way that a plain text search does not answer our question at all without understanding the intent and contextual meaning in the document. [Semantic search](https://en.wikipedia.org/wiki/Semantic_search) is a much better way to solve this issue and it is successfully used by major search engines.

A good starting point is to deploy and integrate an open source search engine, fill it with unstructured data and build analytics on top of it. The most popular search engines are:
- [Elastic Search](https://www.elastic.co/)
- [Solr](http://lucene.apache.org/solr/) 


## Table extraction

On the other hand, tabular data might be easier to be processed by a human. However, if there is a lot of them (imagine thousands of receipts) it can become very exhaustive. Computers are much better at performing these repetitive tasks. Automation of table extraction is the way to tackle this problem. There are some tools that can help:
- [Tabula](http://tabula.technology/)
- [PDF Tables](https://pdftables.com/)
- [pdftableextract](https://github.com/WZBSocialScienceCenter/pdftabextract)

These tools are a good starting point to understand extraction of values from tables. The concrete solution really depends on how complex are the documents that the company needs to process.  


## Classification

Many business processes are based on correct classification of the incoming documents. The employee must first identify and categorize the document before he can decide what to do with it. With the advent of machine learning, classification of documents became available and much more reliable. The pool of open source and commercial text classification tools is still growing and more advanced techniques based on [deep learning](https://en.wikipedia.org/wiki/Deep_learning) are accessible and abstracted in high level machine learning frameworks.

The data preparation steps are as important as training the machine learning classifier itself.

There are various preprocessing steps used in text classification:
- [stemming](https://en.wikipedia.org/wiki/Stemming)
- [lemmatisation](https://en.wikipedia.org/wiki/Lemmatisation)
- splitting to [n-grams](https://en.wikipedia.org/wiki/N-gram)
- removal of [stop words](https://en.wikipedia.org/wiki/Stop_words)


There are 2 common approaches to prepare input for the model: 
- [tf-idf](https://en.wikipedia.org/wiki/Tf%E2%80%93idf "term frequency–inverse document frequency") - term frequency–inverse document frequency
- [word2vec](https://en.wikipedia.org/wiki/Word2vec "Word2vec") - word vectors

The model architecture really depends on experimentation and measuring. Sometimes linear models like [logistic regression](https://en.wikipedia.org/wiki/Logistic_regression) might perform good enough. Other times deep [neural networks](https://en.wikipedia.org/wiki/Artificial_neural_network) might be a better option providing higher  accuracy. It is up to the data science team to explore the documents, define the preprocessing steps, compare various models, tune their parameters and measure the results. 

I recommend these tools as starting points:
- [scikit-learn](http://scikit-learn.org/stable/tutorial/text_analytics/working_with_text_data.html) - basics of text classification
- [Apache Spark MLib](https://spark.apache.org/mllib/) - scalable machine learning library
- [Keras](https://keras.io/) - high level deep learning library
- [PyTorch](http://pytorch.org/) - deep learning framework
- [Gensim](https://radimrehurek.com/gensim/) - topic modeling and text similarity

## Text mining and the business

Many times companies do not realize how much they depend on their unstructured data. Understanding the information in the documents they process every day should not be an IT goal. It should be a business goal. The new benefits that text mining brings to the table, gives the company not only a competitive edge, but also insights into data they already have. The capabilities to quickly find and process documents is essential in the modern competitive market.
Having a text mining team close to the business helps to modernize many business processes.


