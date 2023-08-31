---
title: "Week 9"
---
# Information Retrieval

## Term Selection Techniques
### Tokenisation
- Identify distinct words
- e.g. Separate on whitespace, discard punctuation, fold case

### Stop Word Removal
- Identify high frequency stop words
- Sort terms by collection frequency
- Use stop list to discard words during indexing
- Construct a stop list

### Noun Grouping
- Identify groups of adjacent nouns to index as terms

### Stemming 
- and when generating query terms from query
- Use stemming algorithm to remove affixes from terms before indexing

### Manual Indexing
- Identification of indexing terms by a subject expert

## Vector Model
### Binary Vector Model 
- 1 or 0 if term is present in document

### Vector Model Similarity 
- Determined using the dot product

### Term Weighting
#### Inverse Document Frequency
- $\log_2\frac{\text{total number of documents in collection}}{\text{number of documents that contain the word that we're interested in}}$

#### Term Frequency
- $\frac{\text{number of occurrences of word in document}}{\text{total number of words in document}}$

#### Term Weighting
- TF * IDF

### Rocchio Method
- Query refinement through relevance feedback
- Ask user to tag relevant/non-relevant
- Push towards relevant vectors, away from non-relevant
- $\text{newquery}=(1*\text{query})+(0.75*\text{average of relevant vectors})-(0.25*\text{average of non-relevant vectors})$

## Evaluation
### Precision and Recall
#### Precision
- What fraction of the returned results are relevant to the information need?
- $P(\text{relevant}|\text{retrieved})$

#### Recall
- $P(\text{retrieved}|\text{relevant})$
- What fraction of the relevant documents in the collection were returned by the system?
