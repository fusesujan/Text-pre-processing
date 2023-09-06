# Text Encoding

After acquiring and applying some preprocessing on text data, the next crucial step is text vectorization. Just as images can be represented in numerical form through pixel values and sounds can be represented using frequency values, text also requires a numerical representation that computers can understand.  
However, unlike images and sounds, text presents a unique challenge in this regard. As NLP engineers, it is our responsibility to devise and implement logical methods to convert text into numerical data effectively. The embedding captures semantic relationships and contextual information in the text, making them valuable for tasks such as text classification, sentiment analysis, machine translation, and more.

Encoding text is not an easy problem, and there are many possible ways to do it. Using an effective representation to properly capture the syntax, semantics, and contexts of words can be extremely important for all downstream natural language tasks.

Before we getting into the details, we have to be clear on some of the frequently mentioned NLP terminologies.

**Corpus**: All the words of the dataset.  
**Vocabulary**: Unique words in that corpus.  
**Document**: Each individual sentences or row in perticular data.  
**Word**: Each word as simple as that.

The methods to convert Text into Numerical Vectors i.e Types of text encoding are as follows.

- One hot Encoding
- Index-Based Encoding
- Bag of Words (BOW)
- TF-IDF Encoding
- Word2Vector Encoding
- BERT Encoding

## One hot Encoding

It's used to convert categorical data, such as words or the characters into a binary vector representation. Each unique category (word or character) is represented by a binary vector where only one element is "hot" (set to 1), while all others are "cold" (set to 0).  
Before applying one-hot encoding, you need to tokenize your text data. Once you have tokenized your text, you can proceed with one-hot encoding.  
Next, Build a vocabulary that contains all unique words or tokens present in your corpus. For each word or token in your vocabulary, you create a binary vector of the same length as your vocabulary size. In this binary vector, only one element is set to 1, representing the position of the word in the vocabulary.

For the corpus like: "I work at Fusemachines."

**Vocabulary**: `[ "I", "work" ,"at", "Fusemachines"]`

One hot encoding representation:  
`I : [1 0 0 0]`  
`work : [0 1 0 0]`  
`at : [0 0 1 0]`  
`Fusemachines : [0 0 0 1]`

It is straightforward and easy to implement and each word's representation is independent of other words.  
But the encoded vectors can be very high-dimensional, especially for large vocabularies, which can lead to computational inefficiency and memory usage.
It does not even capture semantic relationships between words. All words are treated as equally dissimilar which causes missunderstanding in data analysis.

## Index Based Encoding:

It is a straightforward method for encoding text data. The concept involves assigning a unique index to each token in the text, allowing us to uniquely identify and represent all tokens within the corpus by their respective index values.
Suppose our corpus include three reviews on company as follows:

##### **corpus** =

    [
      I liked working at Fusemachines.
      Fusemachines has a skilled team.
      Good career opportunities are here.
    ]

**Vocabulary**:

1: "I"  
2: "liked"  
3: "working"  
4: "at"  
5: "Fusemachines"  
6: "has"  
7: "a"  
8: "skilled"  
9: "team"  
10: "Good"  
11: "career"  
12: "opportunities"
13: "are"
14: "here"

The representation become:

"I liked working at Fusemachines." is encoded as `[1, 2, 3, 4, 5]`  
"Fusemachines has a skilled team." is encoded as `[5, 6, 7, 8, 9]`  
"Good career opportunities are here." is encoded as `[10, 11, 12, 13, 14]`

Hence the whole corpus representation become,  
`[  [1, 2, 3, 4, 5]   
    [5, 6, 7, 8, 9]  
    [10, 11, 12, 13, 14]  ] `

Now we have encoded all the words with index numbers, and this can be used as input to any machine since machine understands number.
It is easy to use, no any information loss, replaces the words in each sentence with their respective indexes, nothing more than that.  
But the input should be consistent with the model, ensuring it is the same length as the model, i.e the length of the words in sentences should be equal.If not then This can be achieved by using max padding, where the longest sentence is taken from the document corpus and the other sentences are padded to match. If all of our sentences are `n` words and one sentence is `n+m` words we will make all the sentences of `n+m` words. This ensures that all sentences are equally long.
Also index-based encoding results in high-dimensional sparse vectors. And all words are treated as independent entities, and there is no inherent similarity information encoded in the vectors.

## Bag of words (BOW):

Bag of word involves encoding sentences using the entire data corpus. It is a representation of text that describes the occurrence of words within a document. It is called a “bag” of words, because any information about the order or structure of words in the document is discarded. This only concerned with whether known words occur in the document, not where in the document. BoW is simple to understand and implement, making it a good choice for basic text analysis tasks. BoW can be used with any language since it doesn't rely on language-specific rules or semantics.

From the given corpus first we have to make the Vocabulary ( Collection of unique words ). Now create the document vectors based on the frequency of word in corpus present out thre at particular document.

From above [corpus](#corpus)

**Vocabulary**:
` ['are', 'at', 'career', 'fusemachines', 'good', 'has', 'here', 'liked', 'opportunities', 'skilled', 'team', 'working']`

_Some stopwords are removed here to reduce dimensionality._

**BoW Representation**:

`Sentence 1: [0 1 0 1 0 0 0 1 0 0 0 1] `  
`Sentence 2: [0 0 0 1 0 1 0 0 0 1 1 0] `  
`Sentence 3: [1 0 1 0 1 0 1 0 1 0 0 0] `

Hence the whole corpus representation become,  
`[  [0 1 0 1 0 0 0 1 0 0 0 1]  
    [0 0 0 1 0 1 0 0 0 1 1 0]
    [1 0 1 0 1 0 1 0 1 0 0 0]  ] `

Basically there are two types of BOW ,Simple one and the binary one. Binary BOW we have to encode 1 or 0 for each word appearing or non-appearing in the sentence. Where as in simple we just write the frequency of that each word.

Suppose the corpus is like:  
" I love working with computers, and I love coding.  
I love to do coding in computers. "

Vocabulary:  
`["I", "love", "working", "with", "computers", "and", "coding", "to", "do", "in "]`

Binary BoW of first sentence : `[1 1 1 1 1 1 1 0 0 0]`  
Normal BoW of first sentence : `[2 2 1 1 1 1 1 0 0 0]`

Binary BoW of second sentence : `[1 1 0 0 1 0 1 1 1 1]`  
Normal Bow of second sentence : `[1 1 0 0 1 0 1 1 1 1]`

BoW completely ignores word order and context in a document, which can lead to a loss of valuable information. For example: "The cat chased the dog" and "The dog chased the cat" would have the same BoW representation. BoW doesn't capture word semantics or meaning.  
Also BoW struggles with out-of-vocabulary words that were not seen during training. It's not suitable for tasks requiring deep semantic understanding.

## TF-IDF Encoding:

(Term Frequency-Inverse Document Frequency)  
It is used in information retrieval and text mining to evaluate the importance of a word within a document relative to a collection of documents (i.e corpus). It is a popular technique for text feature extraction and is particularly useful for text classification, document ranking, and information retrieval tasks.

**Term Frequency (TF)**: This component measures how frequently a word appears in a document. It gives higher weight to words that occur more frequently in a document.  
`TF = (Number of times word appears in the document) / (Total  number of words in the document)`

**Inverse Document Frequency (IDF)**: IDF measures the importance of a word in the entire corpus by considering how many documents contain the word. Words that are common across many documents receive lower IDF scores, while words that are rare or unique to a few documents receive higher scores.  
`IDF = log( (Total number of documents in the corpus) / (Number of documents containing the word) )`

**Example Sentences:**
`"I enjoy reading books.",
    "Books provide knowledge."`

Certainly, here's another simple example of calculating TF-IDF for two sentences:

**Example Sentences:**

1. "I enjoy reading books."
2. "Books provide knowledge."

**Step 1: Calculate TF (Term Frequency) for Each Word:**

The TF for each word in each sentence is calculated as the number of times each word appears in the sentence divided by the total number of words in that sentence.

| Word      | Sentence 1 TF | Sentence 2 TF |
| --------- | ------------- | ------------- |
| I         | 1/4           | 0/3           |
| enjoy     | 1/4           | 0/3           |
| reading   | 1/4           | 0/3           |
| books     | 1/4           | 1/3           |
| provide   | 0/4           | 1/3           |
| knowledge | 0/4           | 1/3           |

**Step 2: Calculate IDF (Inverse Document Frequency) for Each Word:**

For this simplified example, let's assume there are only two documents (the two sentences), so IDF is calculated as:

- IDF(word, corpus) = log(2/1)

| Word      | IDF Value |
| --------- | --------- |
| I         | log(2/1)  |
| enjoy     | log(2/1)  |
| reading   | log(2/1)  |
| books     | log(2/1)  |
| provide   | log(2/1)  |
| knowledge | log(2/1)  |

**Step 3: Calculate TF-IDF (Term Frequency-Inverse Document Frequency):**

The TF-IDF for each word is calculated by multiplying its TF and IDF values for each sentence:

| Word      | Sentence 1 TF-IDF | Sentence 2 TF-IDF |
| --------- | ----------------- | ----------------- |
| I         | (1/4) \* log(2/1) | (0/3) \* log(2/1) |
| enjoy     | (1/4) \* log(2/1) | (0/3) \* log(2/1) |
| reading   | (1/4) \* log(2/1) | (0/3) \* log(2/1) |
| books     | (1/4) \* log(2/1) | (1/3) \* log(2/1) |
| provide   | (0/4) \* log(2/1) | (1/3) \* log(2/1) |
| knowledge | (0/4) \* log(2/1) | (1/3) \* log(2/1) |

In above example, the TF-IDF values for each word in both sentences have been calculated. The TF-IDF scores indicate the importance of each word within its respective sentence relative to the entire collection of documents (in this case, the two sentences). Words that are specific to one sentence or carry more weight in the context of the sentence have higher TF-IDF values.

TF-IDF works well with unstructured text data and is not limited to specific document structures or formats. In bigger data common words like "the" and "and" receive low TF-IDF scores due to their high IDF values, which helps reduce their impact on the analysis.

**But**, Like BoW, TF-IDF also ignores word order and context, potentially losing semantic information. The effectiveness of TF-IDF depends on a representative corpus. If the corpus is not diverse or lacks relevant documents, TF-IDF may not work optimally.

## Word2Vector Encoding:

Word2Vec is a popular natural language processing (NLP) technique for generating **word embeddings**, which are vector representations of words in a continuous vector space. Word embeddings capture semantic relationships between words, making them suitable for various NLP tasks like language modeling, sentiment analysis, and machine translation. Word2Vec was introduced by Mikolov et al. in 2013 and has two main algorithms: Continuous Bag of Words (CBOW) and Skip-gram.

Word2vec is not a singular algorithm, rather, it is a family of model architectures and optimizations that can be used to learn word embeddings from large datasets. Embeddings learned through word2vec have proven to be successful on a variety of downstream natural language processing tasks.  
The underlying assumption of Word2Vec is that two words sharing similar rontexts also share a similar meaning and consequently a similar vector representation from the model.

The word2vec tool takes a text corpus as input and produces the word vectors as output. It first constructs a vocabulary from the training text data and then learns vector representation of words. The resulting word vector file can be used as features in many natural language processing and machine learning applications.  
Word2Vec consists of a shallow neural network with a single hidden layer. The input and output layers have a vocabulary size equal to the number of unique words in the corpus. The hidden layer contains the word embeddings.

Intuitive of Word2vec can be explained with two different neural network.
When we have to choose which algorithm to use whether CBOW or Skip-gram , for small data it is preferred to use CBOW as it is fast, where as for large data use Skip-gram .

**In CBOW**: we have to predict target word using context words. Several parameters such as windowsize, vocabsize, etc are defined according to the problem domain. One hot encoding is done for each word input. The output vector (Embedding Dimension) for each word nothing but the weight value of hidden layer to the outer layer.

**In Skip-Gram**: we have to predict context words using target word. Here also several parameters defined. Architectures is exact opposite as CBOW. The output vector (Embedding Dimension) for each word nothing but the weight value of first input layer to the hidden layer.

Both of the algorithms are supervised deep learning algorithm.

**Word Embedding Learning**:
During training, Word2Vec adjusts the word embeddings so that they minimize the difference between predicted and actual context words. This adjustment is performed through backpropagation and gradient descent. The word embeddings are updated iteratively until they converge to meaningful representations.

**Word Vector Similarity**:
Once trained, Word2Vec embeddings have the property that words with similar meanings are close to each other in the vector space. You can calculate the similarity between two word vectors using cosine similarity or other similarity measures.

#### Word2Vec embeddings have various applications:

- **Text Classification**: Enhancing the performance of text classification models.
- **Information Retrieval**: Improving search engine results by understanding semantic relationships.
- **Language Translation**: Aiding in machine translation by capturing word meanings.
- **Recommendation Systems**: Enhancing recommendation algorithms by understanding user preferences.
- **Named Entity Recognition (NER)**: Improving NER models by considering context.

## BERT Encoding

BERT, which stands for Bidirectional Encoder Representations from Transformers, is a powerful pre-trained natural language processing (NLP) model developed by Google AI. All the details regarding this will be explained in next one.
