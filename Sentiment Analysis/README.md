# Sentiment Analysis

## Overview
This project performs **Sentiment Analysis** using Natural Language Processing (NLP) techniques. Sentiment analysis helps determine whether a piece of text expresses a **positive**, **negative**, or **neutral** sentiment. The implementation uses Python libraries such as `NLTK`, `TextBlob`, and `VADER`.

## Features
- **Preprocessing:** Cleans and tokenizes input text.
- **Sentiment Scoring:** Analyzes text to determine sentiment polarity (positive, negative, or neutral).
- **Multiple Approaches:** Uses different NLP libraries (`NLTK`, `TextBlob`, `VADER`).

## Requirements
Ensure you have Python installed, along with the required dependencies:
```sh
pip install nltk textblob vaderSentiment
python -m textblob.download_corpora
```

## Usage
### **Using NLTK & VADER**
```python
import nltk
from nltk.sentiment import SentimentIntensityAnalyzer

# Download necessary data
nltk.download('vader_lexicon')

# Initialize VADER
sia = SentimentIntensityAnalyzer()

# Sample text
text = "I love this product! It's amazing."

# Sentiment scores
sentiment = sia.polarity_scores(text)
print("Sentiment Analysis:", sentiment)
```

### **Using TextBlob**
```python
from textblob import TextBlob

# Sample text
text = "I love this product! It's amazing."

# Analyze sentiment
blob = TextBlob(text)
print("Polarity:", blob.sentiment.polarity)
print("Subjectivity:", blob.sentiment.subjectivity)
```

## Example Output
Using VADER:
```
{'neg': 0.0, 'neu': 0.292, 'pos': 0.708, 'compound': 0.8481}
```
- **Compound Score** > 0: Positive
- **Compound Score** < 0: Negative
- **Compound Score** ≈ 0: Neutral

Using TextBlob:
```
Polarity: 0.85
Subjectivity: 0.75
```
- **Polarity** > 0: Positive
- **Polarity** < 0: Negative
- **Polarity** ≈ 0: Neutral

## License
This project is open-source and free to use.

---
Let me know if you need more details! 🚀

