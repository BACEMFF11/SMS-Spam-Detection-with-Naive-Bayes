# SMS Spam Detection using Naive Bayes

## Introduction
Spam, or unsolicited bulk messaging, has been a persistent issue since the early days of digital communication. It clutters inboxes, poses security risks, and can be used for malicious purposes such as phishing attacks. Effective spam detection is crucial for maintaining the integrity and usability of email systems and other messaging platforms.

This project demonstrates how to build an effective SMS spam classifier using Natural Language Processing (NLP) techniques and the Naive Bayes algorithm.

## Dataset Overview
We'll explore Bayesian spam classification using the SMS Spam Collection dataset, a curated resource tailored for developing and evaluating text-based spam filters. This dataset emerges from the combined efforts of Tiago A. Almeida and Akebo Yamakami at the School of Electrical and Computer Engineering at the University of Campinas in Brazil, and José María Gómez Hidalgo at the R&D Department of Optenet in Spain.

Their work, "Contributions to the Study of SMS Spam Filtering: New Collection and Results," presented at the 2011 ACM Symposium on Document Engineering, aimed to address the growing problem of unsolicited mobile phone messages, commonly known as SMS spam. Recognizing that many existing spam filtering resources focused on email rather than text messages, the authors assembled this dataset from multiple sources, including the Grumbletext website, the NUS SMS Corpus, and Caroline Tag's PhD thesis.

The resulting corpus contains 5,574 text messages annotated as either ham (legitimate) or spam (unwanted), making it an excellent resource for building and testing models that can differentiate meaningful communications from intrusive or deceptive ones. In this context, "ham" refers to messages from known contacts, subscriptions, or newsletters that hold value for the recipient, while "spam" represents unsolicited content that typically offers no benefit and may even pose risks to the user.

## Data Preprocessing

After loading the SMS Spam Collection dataset, the next step is preprocessing the text data. Preprocessing standardizes the text, reduces noise, and extracts meaningful features, all of which improve the performance of the Bayes spam classifier. The steps below rely on the NLTK library for tasks such as tokenization, stop word removal, and stemming.

### Lowercasing the Text
Lowercasing the text ensures that the classifier treats words equally, regardless of their original casing. By converting all characters to lowercase, the model considers "Free" and "free" as the same token, effectively reducing dimensionality and improving consistency.

### Removing Punctuation and Numbers
We selectively remove punctuation marks and numbers that don't contribute significantly to classification, while retaining special characters like '$' and '!' that might be indicative of spam messages.

### Tokenizing the Text
Tokenization splits messages into individual words (tokens), transforming unstructured text into discrete units that can be analyzed independently.

### Removing Stop Words
Stop words are common words like "the," "and," and "is" that appear frequently but carry little semantic meaning for classification purposes. Removing them helps focus the model on more discriminative terms.

### Stemming
Stemming normalizes words by reducing them to their base form (e.g., "running" becomes "run"). This consolidates different forms of the same root word, effectively reducing vocabulary size and smoothing out the text representation. As a result, the model can better understand the underlying concepts without being distracted by trivial variations in word forms.

### Rejoining Tokens
While some ML models work directly with tokens, rejoining them into a space-separated string restores a format compatible with vectorization methods, allowing the dataset to move seamlessly into the feature extraction phase.

## Feature Extraction
CountVectorizer from the scikit-learn library efficiently implements the bag-of-words approach. It converts a collection of documents into a matrix of term counts, where each row represents a message and each column corresponds to a term (unigram or bigram). Before transformation, CountVectorizer applies tokenization, builds a vocabulary, and then maps each document to a numeric vector.

## Model Training and Evaluation
After preprocessing the text data and extracting meaningful features, we train a machine learning model for spam detection. We use the Multinomial Naive Bayes classifier, which is well-suited for text classification tasks due to its probabilistic nature and ability to efficiently handle large, sparse feature sets.

To streamline the entire process, we employ a Pipeline. A pipeline chains together the vectorization and modeling steps, ensuring that the same data transformation (in this case, CountVectorizer) is consistently applied before feeding the transformed data into the classifier. This approach simplifies both development and maintenance by encapsulating the feature extraction and model training into a single, unified workflow.

## Model Deployment
The trained model is saved using joblib, making it easily reusable for future predictions without requiring retraining.

## Conclusion
Our implementation demonstrates the effectiveness of the Naive Bayes algorithm for spam detection. The model successfully identifies various types of spam messages with high probability, showing particular strength in recognizing common spam patterns like promotional offers and suspicious links.

Future improvements could include:
- Exploring more advanced feature extraction techniques like TF-IDF
- Experimenting with different classification algorithms
- Incorporating more features like message length or sender information
- Regularly updating the model with new spam patterns as they emerge
