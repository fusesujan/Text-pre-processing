# Text Cleaning

Text cleaning, also known as text preprocessing or data cleaning, is the process of preparing and refining textual data to make it more suitable for analysis, natural language processing (NLP), or other text-based tasks. Text data often contains noise, inconsistencies, and irrelevant information that can hinder the effectiveness of analysis or machine learning algorithms.

After Data Gathering, sorting, now preparing the data is the most important step in the data analysis process as we know the bad data can have cumulative negative effects further down if it is not corrected.

### Some Common text cleaning tasks are as follows:

**Lowercasing** : Converting all text to lowercase to ensure uniformity in the text data, making it easier to compare and process.  
_Converting "I Am a Machine Learning Engineer." to "i am a machine learning engineer."_

**Tokenization** : Splitting the text into individual words or tokens. This step is crucial for many NLP tasks.  
_Splitting "it's me sujan" into ["it's", "me", "sujan"]_

**Removing special characters**: Eliminating punctuation marks, symbols, or other non-alphanumeric characters that do not provide meaningful information.  
_Removing all non-alphanumeric characters like @,#,$,_, etc.\*

**Stopword removal**: Removing common words (e.g., "the," "and," "in") that occur frequently in the text but typically do not carry much meaning.
\*eg neglecting word like "i","am","a" words from the sentence "i am a machine learning engineer."

**Stemming or Lemmatization**: Reducing words to their base or root form. Stemming simplifies words to their core, while lemmatization ensures that words are transformed to their dictionary form.

**Removing HTML tags and formatting**: If the text data comes from web sources, it may contain HTML tags, which need to be removed.  
Changing the html format code "<p>i am a machine <b>learning</b> engineer.</p>" to "i am a machine learning engineer." format.

**Handling missing data**: Dealing with missing values or placeholders, which may occur in some datasets.  
_Based on the domain knowledge filling up the missing value using valid logic._

**Normalization**: Ensuring consistency in representations of dates, numbers, and other structured information.  
_eg. Changing the date format from "07/01/2023" to '2023-07-01'._

**Spell checking and correction**: Identifying and correcting misspelled words.  
_Converting "i am a maxhine eearning emgineer." to "i am a machine learning engineer."_

**Removing duplicates**: Eliminating duplicate or near-identical text entries that can skew analysis results.

**Text-specific cleaning**: Addressing domain-specific issues or text artifacts that are unique to the dataset or task at hand.
