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

## Analysis
A summary report is displayed to compare the different test accuracies for the different models above.

### TF vs TF-IDF
Using Term Frequency (TF) as text representation and a Naïve Bayes text classifier algorithm achieved a test accuracy of 90.1%. Changing the text representation to TI-IDF while using the same text classifier (Naïve Bayes) slightly improved the test accuracy to 90.2%. This makes sense as TF-IDF supresses uninformative high-frequency terms across documents, resulting in improved performance over (TF) due to better feature discrimination.

### CNN
Using a Convolutional Neural Network (CNN) with random initialised embeddings returned a test accuracy of 89%. This shows that learning embeddings from scratch is not very effective as the model is limited by the dataset’s vocabulary and semantic exposure. The plot of training and test accuracy shows that the model learns very well on training data but starts to overfit after just a few epochs, leading to a drop in test accuracy. This demonstrates the importance of regularisation, splitting the data into validation and test set, and early stopping to balance learning and generalisation

### Pre-trained word embeddings (GloVe)
Using pre-trained word embeddings (GloVe) with 50 dimensions resulted in the highest test accuracy of 90.6%. This shows that the model is able to leverage semantic knowledge from the GloVe embeddings as these embeddings encode semantic and syntactic similarities learned from a large corpus, providing a strong semantic foundation.

### Pre-processing & Hyper-parameter tuning
Three variants of CNN-based classifier models were tested, applying preprocessing, hyperparameter tuning, changing classifiers, and modifying text representations.

The first variant includes preprocessing such as lowercasing texts and removing stopwords, stemming and special character. Early stopping and dropout were added to prevent overfitting. Also, the batch size was decreased, and the number of epochs was increased. An LSTM layer is also added for better text understanding, resulting in a test accuracy of 87.8%. This variant slightly underperformed compared to the CNN + GloVe model, indicating that pre-processing should be avoided for pre-trained
embeddings as it can misalign with the pre-trained vocabularies. Furthermore, LSTM increased the complexity of the model, resulting in poorer performance. 

For the second variant, a deeper CNN with 3 Conv1D layers were tested without LSTM. This deeper architecture showed slightly stronger performance compared to the first variance, with a test accuracy of 88.5%.

For the third variant, a multi-kernel tuning was tested without LSTM. The 3 different kernel sizes were used to help capture different n-gram features. This increased the model’s complexity but didn’t improve the test accuracy. Instead, it has the lowest test accuracy of 79.8%

Overall, while various enhancements such as Bidirectional LSTM, dropout, and multikernel CNNs were explored, none of the tuned models substantially outperformed the simpler CNN + GloVe baseline. The best-performing variant - Deep CNN with GloVe - achieved a test accuracy of 88.5%, slightly below the baseline of 90.6%. This suggests that increased model complexity yielded diminishing returns. 

In summary, pre-trained embeddings like GloVe proved highly effective in capturing generalisable semantic information. Moreover, model tuning does not always lead to improved performance. The marginal drop in accuracy observed in some variants may be attributed to overfitting or over-regularisation introduced during tuning.

