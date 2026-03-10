# YouTube Comment Mental Health & Sentiment Analysis

## Project Overview

This project analyzes emotional patterns and mental health signals in YouTube comments from a depression-themed music video.

Using modern Natural Language Processing (NLP) techniques, the project performs:

- Sentiment analysis using transformer models
- Suicide / mental health signal detection
- Topic modeling to identify discussion themes
- Visualization and statistical analysis of comment patterns

---

## Dataset

The dataset consists of approximately 16k YouTube comments collected from a single depression-themed music video (Source: https://youtu.be/SbNDmAJBtyU?si=9Fqc1fK7c1vYLkpS).

Each comment includes:

- Comment text
- Timestamp (date)
- Number of likes

Example structure:

text| publishedAt| likeCount  
this song saved my life| 2023-10-12| 45  
i feel so alone tonight| 2023-10-13| 12  

---

## Project Pipeline

### 1. Data Collection

Comments are collected using the YouTube Data API.

Steps:

1. Retrieve comments from the selected video
2. Store results in a pandas DataFrame
3. Extract useful fields:
   - text
   - date
   - like count

---

### 2. Data Preprocessing

Data cleaning steps:

- Filter english comments (prob > 0.9)
- Reset dataframe index

---

### 3. Sentiment Analysis

Sentiment analysis is performed using a Transformer-based model.

Model used:

distilbert-base-uncased-finetuned-sst-2-english

This model classifies comments as:

- Positive
- Negative

Example result:

comment| sentiment| confidence  
this song saved me| positive| 0.99  
i feel empty| negative| 0.97  

Implementation is performed using the Hugging Face Transformers library with batch processing.

---

### 4. Suicide / Mental Health Signal Detection

Depression-related comment sections sometimes contain messages indicating mental distress.

A basic detection step identifies comments containing suicide-related language.

Example keywords:

suicide  
suicidal  
kill myself  
want to die  
end my life  
can't go on  

A new feature is created:

suicide_signal = True / False

Example:

comment| suicide_signal  
i feel suicidal tonight| True  
this song helped me| False  

This allows further analysis of high-risk comment patterns.

---

### 5. Topic Modeling

Topic modeling is used to identify common themes in comments.

Method:

BERTopic

Pipeline:

Text  
↓  
Sentence Transformer embeddings  
↓  
Clustering  
↓  
Topic extraction (c-TF-IDF)  

Embedding model:

all-MiniLM-L6-v2

Example topics:

topic| keywords  
Breakup| love, miss, ex  
Loneliness| alone, nobody, cry  
Nostalgia| childhood, memories  
Gratitude| saved, helped  

---

### 6. Suicide Signal Topic Analysis

To better understand high-risk comments, topic modeling can be applied specifically to comments flagged as suicide signals.

Example topics among high-risk comments:

- Breakup / relationship loss
- Loneliness
- Family pressure
- Emotional exhaustion

This step helps reveal context behind distress signals.

---

### 7. Visualization

Several visualizations are generated to understand the dataset.

Sentiment Distribution

Shows the proportion of positive vs negative comments.

Example:

Positive: 55%  
Negative: 45%  

---

Suicide Signal Frequency

Displays how many comments contain potential mental health risk signals.

---

Topic Frequency

Bar chart showing the most common topics detected by BERTopic.

---

## Work in Progress

### Comment Length Analysis

Comparison between:

- normal comments
- suicide signal comments

Observation often seen:

High-distress comments tend to be longer and more detailed.

---

### Community Response Analysis

YouTube comments include like counts, which can be used to measure community engagement.

Example analysis:

type| avg likes  
normal comments| 3  
suicide signal comments| 15  

---

## Temporal Analysis

If timestamps are available, trends can be analyzed over time.

Examples:

- Sentiment change over time
- Suicide signal frequency over time
- Topic popularity trends

Example visualization:

Daily sentiment score  
Daily suicide signal rate  


## German Comments Analysis
Translating foreign-language text into English enables sentiment analysis, and the proposed ensemble model performs better than standalone pre-trained models and LLMs. (source: https://www.nature.com/articles/s41598-024-60210-7).

- Language translation (German comments → English)

Translation enables consistent analysis using English NLP models.

---

## Key Insights


---

## Technologies Used

Python libraries used in the project:

*Python  
pandas  
numpy  
matplotlib  
seaborn  
scikit-learn  
PyTorch  
Hugging Face Transformers  
Sentence Transformers  
BERTopic*  

---

## Project Structure

DepressionCommentAnalysis

*analysisData/ * 
    depression_results.csv

*rawData/ * 
    youtube_comments.csv

*notebooks/  *
    01_data_collection.ipynb  
    02_sentiment_analysis.ipynb  
    03_topic_modeling.ipynb  

*results/  *
    figures/  
    topic_visualizations/  

README.md

---
