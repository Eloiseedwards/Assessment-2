# 1 Introduction

Throughout the project we will work with a dataset of news headlines, each of which had an associated financial sentiment. Our goal is to not only compare predictive performance but to also analyse the practicality of each method in a real-world setting. Financial sentiment prediction
has become a widely researched topic in recent years with NLP models such as BERT increasing in popularity, because sentiment from financial news can be used to
predict stock price movements. Our findings provide guidance to build scalable pipelines for financial sentiment analysis on a small or large scale.  Secondly,
most financial sentiment tasks only have three labels: positive, negative and neutral. This allows for models that indicate the direction of stock movement but not necessarily the magnitude. 
We have increased the granularity of this task by predicting five labels,
adding moderately positive and moderately negative to the set. In a real-world setting this could help build a stock price model that is more sensitive to sentiment prediction.
Whilst the focus of this project on financial sentiment analysis, it provides general advice on how to deal with over fitting, imbalanced data and ordinal classes for neural networks.

Methods we compare include:
*	FinBERT – the financial variant of BERT(Bidirectional Encoder Representations)
*	DistilBERT – the distilled, more efficient variant of BERT
*	Latent Dirichlet Allocation – model used for topic modelling
*	FinGPT – Financial specific generative pretrained transformer, a large language model (LLM)

We chose this selection of models because each posed a solution to one of 3 key identified limitations of finBERT - efficiency (distilBERT), interpretability (LDA) and contextual/numerical reasoning (LLMs).
	
As we are comparing larger, more complex models like FinBERT and FinGPT being specifically designed for tasks such as financial sentiment analysis, and the smaller, simpler models DistilBERT and LDA, we aim to conclude which model can best balance computational efficiency with predictive performance.
