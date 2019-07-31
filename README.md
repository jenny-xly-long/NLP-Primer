# NLP-Primer
Natural Language Processing (NLP) is a tract of Artificial Intelligence and Linguistics devoted to make computers understand statements in human languages. Some useful text and speech processing includes conversational agent, dialogue system, machine translation, question answering, etc.
In this document, I will discuss 4 fields in natural language processing:
1. Information Extraction
2. Text Summarization
3. Machine Translation
4. Semantic Analysis

## Information Extraction
Information extraction (IE) enables automated retrieval of specific information from text. IE depends on Name Entity Recognition to find targeted information to extract, such as LOCATION, PERSON, ORGANIZATION, etc. Once the entities are recognized, algorithms such as relationship extraction, co-reference resolution can then be used to extract its meaning.

### Name Entity Recognition (NER)
NER can automatically scan an entire article and reveal key personnels, organization, location, etc. mentioned in the text. It can also be used to distinguish different meaning of the same term such as Apple the fruit Vs. Apple the company.

The techniques used to perform NER can be characterized in 3 different categories: rule based, feature based and neural based.
#### 1. Rule based
Since ruled based approach is not as often used in industry or in academia, I will not go into too much detail. They are usually used in some very domain specific problems where an exact set of rules and some smaller amount of supervised machine learning can be used to successfully recognized the given entity. For example, if we want to extract the email sender, email receiver and email content from the following string, we can do the following:
<pre><code> Insert code block </code></pre>

#### 2. Feature based 
This approach is to extract features and train a Conditional Random Fields (CRF) sequence model of the same type as part-of-speech (POS) tagging.

#### 3. Neural based

### Topic Modeling
Topic modeling is an unsupervised technique to discover topics across various text documents. It has various applications in different domain. For instance, historians can use it to identify important events in history; web based libraries can use it to recommend books based on your past readings. News providers can leverage the technique to understand articles quickly or to group similar articles.

#### 1. Latent Semantic Analysis (LSA)
#### 2. Latent Dirichlet Allocation (LDA)
LDA is a Bayesian model that uses Dirichlet priors to compute document-topic and word-topic distributions. It has two basic assumptions: <br/>
1. Each document consists of a mixture of topics
2. Each topic consists of a set of words<br/>

LDA considers each document as a collection of topics of different weights. And each topic as a collection of keywords in a certain proportion. Therefore, from LDA's perspective, a topic is nothing but a collection of representative, dominant keywords. You can then infer the topic by looking at the collection of keywords. <br/>

**Logic of LDA: <br/>**
1. Specify the number of topics *N* to discover (note that this is a hyperparameter of the model that we need to fine tune)
2. Randomly assign each word of the documents to one the the *N* topics.
3. Compute the product of P(Topic *T* | Document *D*) [probability of documents *D* assigned to topic *T*] and P(Word *w* | Topic *T*)[probability of topic *T* assignment contributed by word *w*].
4. Re-assign a new topic to each word according to the above result which represents the likelihood that topic *T* would generate word *w*.
5. Repeat steps 3 and 4 until we reach a steady state where topics are assigned correctly according to the computed probability.<br/>

**Example of LDA implementation:**
LDA can be implemented using Sklean or gensim library. I am using gensim and wordnet on the News Category(attach link) dataset. Please see "lda.py" for detailed code. The goal here is to further understand LDA through some code and visualization.

Here is a snapshot of the data set<br/>
![Head of News Category data set](https://user-images.githubusercontent.com/30851539/62175478-e8027c80-b30b-11e9-8a5b-3c86530a28ac.png)

We first preprocess the data by removing the stopwords, tokenizing, lemmatizig and stemming the text.<br/>
![preprocessed_lda_data](https://user-images.githubusercontent.com/30851539/62176348-1897e580-b30f-11e9-953f-4bcfa2a44408.png)

We then match each of the words to a word ID and store them in a dictionary, shown as following<br/>
![lda_dic](https://user-images.githubusercontent.com/30851539/62176473-affd3880-b30f-11e9-8778-c5ae016c849c.png)

Given the following example from the data set, we can count the number of times that each words occured in the sentence.
[insert photo]

Finally, we build the LDA model by choosing the number of topics. And it prints the 40 topics as below:
[insert photo]
As we can see, each topic is just a combination of words associated with different weights to show its significance.
For the chosen example, its assigned topics are:<br/>
[insert photo]
We can then infer its topic may be "Police shoots and kills black lives".
Here is a great visualization of LDA created by pyLDAvis library. Ideally, the topic bubble should not be overlapping. If the topics are too crowded, it may be an indicator that the number-of-topic parameter is set too high.<br/>
![lda_vis](https://user-images.githubusercontent.com/30851539/62178213-269d3480-b316-11e9-8547-7ba1ada5f74c.gif)

### Event Extraction (EE)
EE gathers knowledge about periodical incidents found in texts, automatically identifying information about what happed and when it happened. The amount of text generated daily are enormous. Being able to extract key information from a giant pool of data can help us be more efficient. For example, extracting events from business news aids users to perceive market trends, stay up to date with competitors' strategies and to make valuable investment decisioins.
