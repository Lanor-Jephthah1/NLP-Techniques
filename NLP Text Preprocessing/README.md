# TripAdvisor Hotel Review Analysis Project

This project aims to analyze TripAdvisor hotel reviews using various Natural Language Processing (NLP) techniques. It covers text preprocessing, tokenization, stemming, lemmatization, and n-gram analysis to gain insights into the most common words and phrases used in the reviews.

## Project Overview

The dataset consists of hotel reviews from TripAdvisor, each with an associated rating. The goal of this project is to process and analyze the text data using multiple NLP techniques, which include:

- **Text Preprocessing**: Convert text to lowercase, remove stopwords, handle punctuation.
- **Tokenization**: Break text into individual tokens (words).
- **Stemming**: Reduce words to their root forms using a stemming algorithm.
- **Lemmatization**: Normalize words to their base or dictionary forms.
- **N-gram Analysis**: Analyze unigrams (single words) and bigrams (pairs of words) to identify frequently occurring terms and phrases.

## Dataset

The dataset used in this project consists of 109 hotel reviews, each accompanied by a rating. The dataset has the following columns:

- **Review**: The text of the hotel review.
- **Rating**: The rating given to the hotel (from 1 to 5).

## Text Preprocessing Steps

1. **Lowercasing**: Convert all the text in the reviews to lowercase.
2. **Stopword Removal**: Remove common words (like "the", "is", "and") that don't contribute significant meaning, except for the word "not" to preserve negations.
3. **Punctuation Removal**: Remove punctuation marks from the text.
4. **Tokenization**: Split the reviews into individual words (tokens).
5. **Stemming**: Reduce words to their base form using the Porter Stemmer.
6. **Lemmatization**: Normalize words to their base form using the WordNet Lemmatizer.

## Exploratory Data Analysis (EDA)

### Most Frequent Unigrams (Top 10)

The most frequent unigrams (single words) in the reviews:

```text
(hotel,)       292
(room,)        275
(great,)       126
(not,)         122
(stay,)         95
(staff,)        90
(nt,)           81
(seattle,)      79
(location,)     78
(good,)         76
```

### Most Frequent Bigrams (Top 10)

The most frequent bigrams (pairs of words) in the reviews:

```text
(great, location)      24
(space, needle)        21
(hotel, monaco)        16
(great, view)          12
(staff, friendly)      12
(great, hotel)         12
(pike, place)          12
(location, great)      10
(walking, distance)    10
(king, bed)             9
```

## Code Walkthrough

### Step 1: Data Preprocessing

Convert all the review text to lowercase:

```python
data["review_lowercase"] = data.Review.str.lower()
```

### Step 2: Stopword Removal

Remove stopwords from the reviews, preserving the word "not":

```python
en_stopwords = stopwords.words("english")
en_stopwords.remove("not")
data["review_no_stopwords"] = data["review_lowercase"].apply(lambda x: " ".join(word for word in x.split() if word not in en_stopwords))
```

### Step 3: Tokenization

Tokenize each review into individual words:

```python
data["tokenized"] = data.apply(lambda x: word_tokenize(x["review_no_stopwords_no_punct"]), axis=1)
```

### Step 4: Stemming and Lemmatization

Apply stemming using the PorterStemmer and lemmatization using the WordNetLemmatizer:

```python
ps = PorterStemmer()
data["stemmer"] = data["tokenized"].apply(lambda tokens: [ps.stem(token) for token in tokens])

lemmatizer = WordNetLemmatizer()
data["lemmatized"] = data["tokenized"].apply(lambda tokens: [lemmatizer.lemmatize(token) for token in tokens])
```

### Step 5: N-Grams Analysis

Generate unigrams and bigrams, then display the top occurrences:

```python
unigrams = pd.Series(nltk.ngrams(tokens_clean, 1)).value_counts()
bigrams = pd.Series(nltk.ngrams(tokens_clean, 2)).value_counts()
```

## Visualization

A bar chart is generated to visualize the top 20 most frequent bigrams:

```python
bigrams[:20].sort_values().plot.barh(color="lightsalmon", width=.9, figsize=(12, 8))
```

## How to Run

1. Clone the repository:

   ```bash
   git clone https://github.com/Lanor-Jephthah1/TripAdvisor-Hotel-Review-Sample-Project.git
   ```

2. Install the required libraries:

   ```bash
   pip install -r requirements.txt
   ```

3. Run the script:

   ```bash
   python tripadvisor_reviews.py
   ```

## Dependencies

The following libraries are required to run this project:

- pandas
- nltk
- matplotlib
- re

## License

This project is licensed under the MIT License.

### Key Updates:
- Detailed explanations of each step in the preprocessing pipeline.
- Explanation of the analysis performed (unigrams and bigrams).
- Example outputs for unigrams and bigrams.
- A concise "How to Run" section for easy usage by others.
