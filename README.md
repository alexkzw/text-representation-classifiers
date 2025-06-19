# text-representation-classifiers

This project applies different key text representation techniques and evaluate their performance using different classifiers.

## Dataset

The dataset used is the AG News dataset, a subset of AG's corpus of news articles. The dataset consists of titles and descriptions from four major classes: “World”, “Sports”, “Business”, and “Sci/Tech”. It includes 30,000 training samples and 1,900 test samples per class. 

- A text classifier is built using **Term Frequency** (TF) as text representation & Naive Bayes as the classifier algorithm.
- Another text classifier is built using **TF-IDF** as text representation & Naive Bayes as the classifier algorithm.
- Another text classifier is built using **Convolutional Neural Network** (CNN).
- Another CNN-based text classifier is built using **pre-trained word embeddings** (GloVe).
- Another CNN-based text classifier is built by applying data preprocessing, hyperparameter tuning and changing classifiers.

## Pre-processing
- Pre-processing includes lowercasing all words, removing stop-words and stemming, tokenising and pad sequences to fixed length.
- Early-stopping is added for training stability and to avoid overfitting.

## Hyper-parameter tuning
- Dropout is added to CNN model to prevent overfitting.
- A Bi-directional LSTM layer after CNN is added for better text understanding (enables reading context from both directions).
- Learning rate is lowered to reduce oscillation and better refinement.
- A deeper CNN (3 Conv1D layer) without LSTM was implemented.
- Dropout was added to force the network to spread its representation across different neurons, preventing a small group of neurons from becoming over-specialised.
- Global Max-Pooling was added to reduce dimension while capturing the strongest signal.
- Multi-kernel CNN model (kernel sizes of 3,4,5) were tested to capture different n-gram features.

A summary report is displayed to compare the different test accuracies for the different models above.
