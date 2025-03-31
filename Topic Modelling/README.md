# Topic Modelling

## Overview
Topic Modelling is an **unsupervised machine learning technique** used to discover hidden topics in large collections of text. It helps in understanding document structures by clustering similar words into coherent topics. Common algorithms for topic modelling include **Latent Dirichlet Allocation (LDA)** and **Non-Negative Matrix Factorization (NMF)**.

## Features
- **Unsupervised Learning**: No labeled data is required.
- **Extracts Hidden Themes**: Identifies recurring patterns of words.
- **Scalability**: Works with large text corpora.
- **Applications**: Used in news categorization, content recommendation, and text summarization.

## Requirements
Ensure you have Python installed along with the necessary dependencies:
```sh
pip install numpy pandas scikit-learn gensim nltk
```

## Usage
### **Step 1: Import Libraries**
```python
import numpy as np
import pandas as pd
from sklearn.feature_extraction.text import CountVectorizer, TfidfVectorizer
from sklearn.decomposition import LatentDirichletAllocation
import nltk
from nltk.corpus import stopwords
```

### **Step 2: Define and Preprocess Text Corpus**
```python
nltk.download('stopwords')
stop_words = stopwords.words('english')

documents = [
    "Machine learning is fascinating and used in AI.",
    "Deep learning improves AI capabilities.",
    "Natural language processing is a subset of AI.",
    "Topic modelling discovers hidden themes in documents."
]

vectorizer = CountVectorizer(stop_words=stop_words, ngram_range=(1,2))
X = vectorizer.fit_transform(documents)
```

### **Step 3: Apply Latent Dirichlet Allocation (LDA)**
```python
lda_model = LatentDirichletAllocation(n_components=2, random_state=42)
lda_model.fit(X)

# Display Topics
def display_topics(model, feature_names, num_words):
    for topic_idx, topic in enumerate(model.components_):
        print(f"Topic {topic_idx + 1}:")
        print(" ".join([feature_names[i] for i in topic.argsort()[:-num_words - 1:-1]]))
        print()

display_topics(lda_model, vectorizer.get_feature_names_out(), 5)
```

## Example Output
```
Topic 1:
ai deep learning machine fascinating

Topic 2:
natural language processing topic modelling documents
```
- Each topic consists of the most significant words.
- The LDA model assigns probabilities to documents belonging to topics.

## Advanced Techniques
### **1. Using TF-IDF for Better Features**
```python
tfidf_vectorizer = TfidfVectorizer(stop_words=stop_words, ngram_range=(1,2))
X_tfidf = tfidf_vectorizer.fit_transform(documents)
lda_tfidf = LatentDirichletAllocation(n_components=2, random_state=42)
lda_tfidf.fit(X_tfidf)
display_topics(lda_tfidf, tfidf_vectorizer.get_feature_names_out(), 5)
```

### **2. Using Non-Negative Matrix Factorization (NMF)**
```python
from sklearn.decomposition import NMF
nmf_model = NMF(n_components=2, random_state=42)
nmf_model.fit(X)
display_topics(nmf_model, vectorizer.get_feature_names_out(), 5)
```

## Use Case Examples
- **News Categorization**: Grouping articles into topics such as politics, sports, or technology.
- **Customer Reviews Analysis**: Identifying common themes in customer feedback.
- **Academic Research**: Summarizing large sets of research papers into topics.

## Limitations
- **Topic Interpretability**: Topics may not always be human-interpretable.
- **Requires Fine-Tuning**: The number of topics and preprocessing steps need optimization.
- **Context Loss**: Ignores word order and sentence structure.

## License
This project is open-source and free to use.

---


