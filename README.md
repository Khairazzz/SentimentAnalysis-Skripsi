# AI-Based Sentiment Analysis and User Feedback for UI/UX Improvement

An end-to-end Natural Language Processing (NLP) project that analyzes user reviews of the **iPusnas mobile application** from Google Play Store to identify user sentiment, discover major discussion topics, and generate insights for improving the application experience.

The project combines **IndoBERT-based sentiment classification**, traditional machine learning baselines, and **BERTopic** to transform large-scale user reviews into actionable UI/UX insights.

---

## 📌 Project Overview

User reviews contain valuable information about how users experience a digital product. However, manually analyzing thousands of reviews is inefficient and makes it difficult to identify recurring problems and priorities.

This project aims to answer two main questions:

1. **What is the sentiment expressed by users in their reviews?**
2. **What aspects of the application are most frequently discussed by users, and what can be improved based on those reviews?**

The analysis follows an end-to-end pipeline:

```text
Google Play Reviews
        ↓
Data Collection
        ↓
Text Preprocessing
        ↓
Sentiment Classification
        ↓
Sentiment Analysis
        ↓
BERTopic
        ↓
Topic Identification
        ↓
7 UI/UX Aspects for negative sentiment
        ↓
User Feedback & Improvement Insights
        ↓
Prototype Improvement Recommendation 
```

---

## 🎯 Objectives

* Analyze user sentiment from large-scale Indonesian app reviews.
* Compare the performance of **IndoBERT** with traditional machine learning approaches.
* Identify recurring topics in user feedback using **BERTopic**.
* Group discovered topics into meaningful **UI/UX aspects**.
* Identify areas that require attention based on user feedback.
* Transform unstructured user reviews into actionable product insights.

---

## 📊 Dataset

The dataset consists of user reviews collected from the **Google Play Store for the iPusnas application**.

| Information                 | Details                         |
| --------------------------- | ------------------------------- |
| Application                 | iPusnas                         |
| Data Source                 | Google Play Store               |
| Review Period               | August 16, 2016 - June 11, 2026 |
| Reviews Collected           | 20,645                          |
| Reviews Used for Prediction | 16,733                          |
| Positive Reviews            | 2,008                           |
| Negative Reviews            | 14,725                          |
| Language                    | Indonesian                      |

The final dataset used for sentiment prediction contains a substantial proportion of negative reviews, providing an opportunity to investigate the major issues experienced by users.

> **Note:** The raw dataset is not included in this repository.

---

## 🧠 Methodology

### 1. Text Preprocessing

The review data was prepared before being used for model training and topic modeling.

The preprocessing pipeline includes:

* Text cleaning
* Tokenization
* Data preparation
* Label preparation
* IndoBERT tokenization
* Sequence truncation with a maximum length of 128 tokens

---

### 2. Sentiment Classification

Three approaches were evaluated:

#### IndoBERT

A pretrained Indonesian language model was fine-tuned for sentiment classification.

**Configuration:**

| Parameter               |    Value |
| ----------------------- | -------: |
| Model                   | IndoBERT |
| Batch Size              |       16 |
| Epochs                  |        5 |
| Learning Rate           |     2e-5 |
| Maximum Sequence Length |      128 |

---

## 📈 Model Performance

The model was evaluated using classification metrics.

|              |  Precision |   Recall   |   F1-Score |   Support  |
| ----------   | ---------: | ---------: | ---------: | ---------: |
| Accuracy     |            |            | **98.74%** |     397    |
| Macro avg    |   94.48%   |   84.49%   |   88.81%   |     397    |
| Weighted avg |   98.67%   |   98.74%   |   98.66%   |     397    |

### Confusion Matrix

The confusion matrix below shows the classification performance of the final sentiment classification model.

<img width="627" height="454" alt="Gambar 4 19  Confusion Matrix Hasil Klasifikasi" src="https://github.com/user-attachments/assets/86a21d6f-2120-4eea-94b4-a1e7d9c4aed5" />

![Confusion Matrix](results/confusion_matrix.png)

---

## 📊 Sentiment Distribution

After applying the sentiment classification model to the final dataset, the predicted sentiment distribution was:

| Sentiment |    Reviews | Percentage |
| --------- | ---------: | ---------: |
| Negative  |     14,725 |        88% |
| Positive  |      2,008 |        12% |
| **Total** | **16,733** |   **100%** |

The distribution indicates that **negative feedback dominates the collected reviews**, suggesting that users frequently encountered issues or dissatisfaction when using the application.

<img width="400" height="406" alt="Gambar 4 21  Distribusi Prediksi Sentimen Seluruh Dataset" src="https://github.com/user-attachments/assets/f3d31e69-a1db-4c50-9db7-e596a1d85c6c" />

![Sentiment Distribution](results/sentiment_distribution.png)

---

# 🔎 Topic Modeling with BERTopic

Sentiment classification identifies **whether users are positive or negative**, but it does not explain **what users are talking about**.

To investigate the content of user feedback, **BERTopic** was used to discover recurring topics within the reviews for **negative sentiment only**.

### Topic Modeling Pipeline

```text
User Reviews
     ↓
Sentence Embedding
     ↓
UMAP
     ↓
HDBSCAN
     ↓
BERTopic
     ↓
24 Identified Topics
     ↓
Topic Interpretation
     ↓
7 UI/UX Aspects
```

The topic modeling process identified **24 topics**, with a portion of the reviews classified as noise by the clustering algorithm.

Approximately **6,012 negative reviews (40.8%)** were not assigned to a specific topic.

---

## 🖥️ UI/UX Aspects

The discovered topics were interpreted and consolidated into **7 major UI/UX aspects**:

| No. | UI/UX Aspect                | Keyword                                                                 |
| --: | --------------------------- | --------------------------------------------------------------------------- |
|   1 | **Application Performance** | Loading speed, crashes, responsiveness, and overall application performance |
|   2 | **Book Collection**         | Book availability, collection, search, and access to digital books          |
|   3 | **Interface / UI**          | Visual interface, navigation, layout, and usability                         |
|   4 | **Login & Account**         | Authentication, registration, account access, and login-related issues      |
|   5 | **Reading Experience**      | Reading interface, book display, page navigation, and reading functionality |
|   6 | **Server & Connectivity**   | Server availability, connection problems, and network-related issues        |
|   7 | **Application Updates**     | Updates, changes in application versions, and issues following updates      |

---

## 📊 Sentiment by UI/UX Aspect

To provide more actionable insights, sentiment was analyzed within each identified UI/UX aspect.

This analysis helps distinguish between aspects that are frequently discussed and aspects that receive predominantly negative feedback.

<img width="1187" height="707" alt="Gambar 4 25 Distribusi Ulasan Negatif per Aspek" src="https://github.com/user-attachments/assets/df8f78b0-1a71-4d11-89b2-fd1002dc3e80" />

![Sentiment Distribution by UI/UX Aspect](results/sentiment_by_aspect.png)

### Example Interpretation

The sentiment distribution can be used to identify which aspects require greater attention.

For example:

```text
High Negative Sentiment
        ↓
Potential User Pain Point
        ↓
Investigate Common Complaints
        ↓
Identify Root Cause
        ↓
UI/UX Improvement Recommendation
```

This allows the analysis to move beyond simply classifying reviews into positive and negative categories and instead provides a **product-oriented perspective on user feedback**.

---

# 💡 Key Insights

The analysis demonstrates several important findings:

### 1. Negative feedback dominates the dataset

The majority of analyzed reviews were classified as negative, indicating that users frequently expressed dissatisfaction with the application.

### 2. IndoBERT achieved the best classification performance

IndoBERT achieved an accuracy of **98.74%**, outperforming the traditional machine learning baselines evaluated in this project.

### 3. User feedback covers multiple aspects of the application

BERTopic identified **24 topics**, which were subsequently interpreted and consolidated into **7 major UI/UX aspects**.

### 4. Sentiment analysis and topic modeling complement each other

Sentiment classification answers:

> **"How do users feel?"**

Topic modeling answers:

> **"What are users talking about?"**

Combining both provides a more comprehensive understanding of user feedback.

---

# 🛠️ Tech Stack

**Programming Language**

* Python

**Natural Language Processing**

* IndoBERT
* Transformers
* Sentence Transformers
* BERTopic

**Machine Learning**

* Scikit-learn

**Topic Modeling**

* BERTopic
* UMAP
* HDBSCAN
* `paraphrase-multilingual-MiniLM-L12-v2`

**Data Processing & Visualization**

* Pandas
* NumPy
* Matplotlib
* Seaborn

**Environment**

* Google Colab / Jupyter Notebook

---

# 📚 Project Context

This project was developed as part of an undergraduate thesis in **Information Technology at Universitas Gadjah Mada**.

The project focuses on combining **Natural Language Processing, Machine Learning, and user feedback analysis** to support a more user-centric approach to application improvement.

---

# 👩🏻‍💻 Author

**Ovie Khaira**

Information Technology
Universitas Gadjah Mada
