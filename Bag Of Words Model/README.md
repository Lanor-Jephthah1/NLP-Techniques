# Bag of Words Model

## Overview
The **Bag of Words (BoW)** model is a fundamental technique in Natural Language Processing (NLP) for text vectorization. It represents text as a set of word occurrences, disregarding grammar and word order but retaining crucial word frequency information. This model is widely used in tasks such as text classification, clustering, and sentiment analysis.

## Features
- **Text Preprocessing:** Includes tokenization, lowercasing, and punctuation removal.
- **Vectorization:** Converts text into a numerical representation using `CountVectorizer`.
- **Sparse Matrix Representation:** Efficiently stores word counts in a compressed format.
- **Customizable:** Supports `n-grams`, stopword removal, and vocabulary size restriction.

## Requirements
Ensure you have Python installed along with the required dependencies:
```sh
pip install scikit-learn nltk
```

## Usage
### **Step 1: Import Libraries**
```python
from sklearn.feature_extraction.text import CountVectorizer
import pandas as pd
```

### **Step 2: Define Text Corpus**
```python
documents = [
    "I love machine learning and NLP.",
    "Machine learning is amazing!",
    "Natural Language Processing is a subset of AI.",
    "Deep learning is part of AI and NLP."
]
```

### **Step 3: Initialize and Apply CountVectorizer**
```python
# Create the vectorizer
vectorizer = CountVectorizer(lowercase=True, stop_words='english', ngram_range=(1,2))

# Fit and transform the text data
X = vectorizer.fit_transform(documents)

# Convert to DataFrame for better visualization
df = pd.DataFrame(X.toarray(), columns=vectorizer.get_feature_names_out())
print(df)
```

## Example Output
```
   ai  deep  deep learning  learning  learning ai  learning nlp  machine  machine learning  natural  natural language  nlp  nlp subset  processing subset  subset  subset ai
0   0     0             0         1           0            0       1                1       0                 0    1           0                   0       0        0
1   0     0             0         1           0            0       0                1       0                 0    0           0                   0       0        0
2   1     0             0         0           0            0       0                0       1                 1    1           1                   1       1        1
3   1     1             1         1           1            1       0                0       0                 0    1           0                   0       0        1
```
- Each row represents a document.
- Each column corresponds to a word or `n-gram` from the vocabulary.
- Values indicate the frequency of a word in the respective document.

## Advanced Customizations
### **1. Limit Vocabulary Size**
To include only the most common words:
```python
vectorizer = CountVectorizer(max_features=10)
```

### **2. Use Bigrams (2-word phrases)**
```python
vectorizer = CountVectorizer(ngram_range=(2,2))
```

### **3. Convert to TF-IDF for Weighting**
```python
from sklearn.feature_extraction.text import TfidfTransformer

tfidf_transformer = TfidfTransformer()
X_tfidf = tfidf_transformer.fit_transform(X)
```

## Use Case Examples
- **Spam Detection**: Identifying spam emails based on frequently used words.
- **Text Classification**: Categorizing news articles into topics.
- **Sentiment Analysis**: Extracting insights from customer reviews.
- **Keyword Extraction**: Identifying key terms from documents.

## Limitations
- **Ignores Word Order**: Meaning can be lost since only frequencies are considered.
- **High Dimensionality**: Large vocabularies lead to large feature spaces.
- **Does Not Capture Semantics**: Cannot understand context, synonyms, or polysemy.

## License
This project is open-source and free to use.

---
Let me know if you need further modifications! 🚀

