---
title: Large Scale Image Search
---

# Text Information Retrieval
## Weighting the Vectors
The number of times a word occurs in a document reflects the importance of that word in the document
### Possible Weighting Schemes
#### Term Frequency - Inverse Document Frequency (TF-IDF)
Inverse Document Frequency - Provides high values for rare words and low values for common words
##### Term Frequency
The frequency count of a term in a document
##### Raw Frequency
Frequency of occurrence of term in document included in vector
##### Binary Weights
Only uses the presence (1) or absence (0) of a term recorded in a vector
### Weighting Intuitions
- A term that appears in many documents is not important
	- e.g. the, going, come, ...
- If a term is frequent in a document, and rare across other documents, it is probably important in that document
## Bag of Words Vectors
Each word in the documents bag of words, contributes a count to the corresponding element of the vector for that word
- Each vector is effectively a histogram of the word occurrences in the respective document
- Vectors will have a high number of dimensions, but be very sparse
We create vectors for each document with as many dimensions as there are words in the lexicon
The lexicon/vocabulary is the set of all processed words across all documents known to the system
## The Vector-Space Model
- Model each document by a vector
- Model each query by a vector
- Assumes documents that are "close together" in space are similar in meaning
- Use standard similarity measures to rank each document to a query in terms of decreasing similarity
## Inverted Indexes
- A map of words to lists of postings
- A posting is a pair formed by a document ID and the number of times that specific word appeared in that document
- Computing the Cosine Similarity
	- For each word in the query, lookup the relevant postings list and accumulate similarities, for only the documents seen in those postings lists
	- ![|400](https://remnote-user-data.s3.amazonaws.com/Uz8GJyOeswkTWxzGkpEcN0C1eUw8tDFKCzwpX0WzIf-GyuT0QK8W05afo1rrRxvJ18zD5W9RofWtb5e89NbLXMiWKejCHmsuK6HsW8ODcbzx9AenWhSQCJIV_X3dryJg.png) 
![|400](https://remnote-user-data.s3.amazonaws.com/e16xDON3GPBEJolFKH2_ur8AOdP8GYcXR2VXkm4aHU5F_MC3aeJjbh3HMLvbHzcHfdpw-HfsCIaymhCAe8iwKABr1YC7hl21XG7hOgmtytpLm4gr9KNcqW-3nzPHuglP.png) 
## Searching the Vector Space Model
Given a query you can find a match by measuring the distance between vectors
The query vector will be significantly shorter than the bag of words vectors, so distance is measured using the cosine similarity
![|400](https://remnote-user-data.s3.amazonaws.com/Uw47pGONuOQ087vA-W3uU1-V1yn12R8qn8mLOwxzzmjC54FsZi-jYqR20TPaELofAatKg6lWdxYWgkKCqUtHA-OlOI2H8kM6jnXzoh7jMhAEgq6IwC6GQyOfiP4aAUIg.png) 
## The Bag Data Structure
### Bag of Words
![|400](https://remnote-user-data.s3.amazonaws.com/kDACx4-c0DNVu41Ba9uR_33hnxszH3ZBUhtDbJE3_9G6xf_NFnBi9uWhaslgnFSv7FTBKp9wkSbYJgUVSDD0xSgJY_hswlmo3UtCF_IDfJc6wLsthpG2iXu3fnWb14Ps.png) 
A bag is an unordered data structure like a set which, unlike a set, allows elements to be inserted multiple times
- Sometimes called a multiset or a counted set
## Text Processing (Feature Extraction)
- Stop-word Removal (Optional) - Removing words like "the"
- Tokenisation
- Stemming/Lemmatisation (Optional) - Reducing words to their stem
	- e.g. Jumped - > Jump
- Bag of Words
#### Example 
![|400](https://remnote-user-data.s3.amazonaws.com/f_kuHYqqGco0sxCNX2u43bNgwupI3JtVwjWrksaw1zjbC7y69pvFWvNSrd8w170kwcnZfHdwKRbbYnfxD78EQeK96OEQy_hsiQDN7aheD-5M6vYSsrrfROzWn_FOt03P.png) 
## Vector Quantisation
Vector quantisation is achieved by representing a vector by another approximate vector
![|400](https://remnote-user-data.s3.amazonaws.com/gxe0eY5PtTjZnSNO8tzcb2E_O0yFcEcuNiu1Pu9kog49eSjT7MgRrxkghsJpOR_C3auZySNsBTaaDw7bolJvmL9lJ26SsUGyH6um-6pJSOHHOnNBiSQ5r_h6TIR_vEll.png) 
- Each input vector is assigned to the nearest vector from the pool of representative vectors
### Learning a Vector Quantiser
- Vector quantisation is a lossy data compression technique
- Given a set of vectors, a technique like k-means clustering can be used to learn a fixed size set of representative vectors
	- The representatives are the mean vector of each cluster in k-means
	- The set of representation vectors is called a codebook
![|400](https://remnote-user-data.s3.amazonaws.com/jIxoTIAowUE0KWqrc40o-zhQjhmbTZooyPivBbcKd5JY6UslisOPqcS6b-oZiSmtddVF1Cm-cQhRlFE0ZLMN26CGWqN4MW1h6f9jEzKdD9BSM2Du88AlFf_ujIscbruM.png) 

# Visual Words
## SIFT Visual Words
- We can vector quantise SIFT descriptors
	- The codebook is the visual equivalent of a lexicon or vocabulary
	- Each descriptor is replaced by a representative vector known as a visual word
		- The process of applying vector quantisation to local features is similar to the stemming of words
		- The visual word describes a small image patch with a certain pattern of pixels
## Bags of Visual Words
Once we've quantised the local features into visual words, they can be put into a bag
- This is the Bag of Visual Words (BoVW)
- We effectively ignore the location of the local features in the original image
## Histograms of Bags of Visual Words
Once we have a BoVW and knowledge of the complete vocabulary (the codebook), we can build histograms of visual word occurrences
This provides a way of aggregating a variable number of local descriptors into a fixed length vector
- Useful for machine learning
- Also allows us to apply techniques for text retrieval to images
![|400](https://remnote-user-data.s3.amazonaws.com/TKu6VE3h-7QptAlkuDlW9o7txvCTEF7SH6kYExyjMVUEaAhBNzL13aYlFQmS4RhebHxToctThpA6mpDmfLwecxzRYEhxqP1e9Q57-stx-YnDtDX3ctLMulsbr1QsLnVs.png) 
## The Effect of Codebook Size
The size of the vocabulary is a key parameter in building visual word representations
- Too small means all vectors look the same, not distinctive
- Too big means the same visual words might never appear across images, too distinctive

# Content-Based Image Retrieval
## Overall Process for Building a BoVW Retrieval System
1. Vector quantise the features, and build BoVW representations for each image
2. Learn a large codebook from a sample of features
3. Collect the corpus of images that are to be indexed and made searchable
4. Construct an inverted index with the BoVW representations
5. Extract local features from each image
## Optimal Codebook Size
Inverted indexes only give a performance gain if the vectors are sparse
Visual words also need to be sufficiently distinctive to minimise mismatching
- Large codebooks cause problems as they are non-trivial
- Implies a very large codebook size
![|400](https://remnote-user-data.s3.amazonaws.com/cxElqQaN10VcAZKh_dyNO0iT6uGDUz84XeDMwSDngrAoR38M2n2wTdk1iL5GRMRB40kcEn9n9cKrT7KVKb3xAsEiPAYZtufcRxidm6XWxfWMoaORvjx62zFqzwArZZ4k.png) 
## BoVW Retrieval
With the visual word representation, everything used for text retrieval can be applied directly to images
- Inverted index
- Vector space model
- Weighting schemes
- Cosine simularity