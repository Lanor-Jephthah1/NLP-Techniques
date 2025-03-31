# POS and NER Recognition

## Overview
This project performs **Part of Speech (POS) tagging** and **Named Entity Recognition (NER)** using Natural Language Processing (NLP) techniques. The implementation uses Python libraries such as `spaCy` and `NLTK` to analyze text.

## Features
- **POS Tagging**: Identifies the part of speech (e.g., noun, verb, adjective) of each word in a given text.
- **NER**: Extracts named entities such as names, organizations, dates, and locations.

## Requirements
Ensure you have Python installed, along with the required dependencies:
```sh
pip install spacy nltk
python -m spacy download en_core_web_sm
```

## Usage
### **Using spaCy**
```python
import spacy

# Load spaCy's English model
nlp = spacy.load("en_core_web_sm")

# Input text
doc = nlp("Apple is looking at buying U.K. startup for $1 billion")

# POS Tagging
print("POS Tagging:")
for token in doc:
    print(f"{token.text}: {token.pos_}")

# Named Entity Recognition
print("\nNamed Entities:")
for ent in doc.ents:
    print(f"{ent.text}: {ent.label_}")
```

### **Using NLTK**
```python
import nltk
from nltk.tokenize import word_tokenize
from nltk import pos_tag, ne_chunk

nltk.download("punkt")
nltk.download("averaged_perceptron_tagger")
nltk.download("maxent_ne_chunker")
nltk.download("words")

# Input text
text = "Apple is looking at buying U.K. startup for $1 billion"

# Tokenization
tokens = word_tokenize(text)

# POS Tagging
pos_tags = pos_tag(tokens)
print("POS Tagging:")
print(pos_tags)

# Named Entity Recognition
ner_tree = ne_chunk(pos_tags)
print("\nNamed Entities:")
print(ner_tree)
```

## Example Output
**POS Tagging:**
```
Apple: PROPN
is: AUX
looking: VERB
at: ADP
buying: VERB
U.K.: PROPN
startup: NOUN
for: ADP
$1: NUM
billion: NUM
```

**Named Entities:**
```
Apple: ORG
U.K.: GPE
$1 billion: MONEY
```

## License
This project is open-source and free to use.

---
Let me know if you need any modifications! 🚀

