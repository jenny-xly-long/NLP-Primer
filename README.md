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

Here is one example from the data set, we can see if any of the words in the dictionary occured in this sentence and we can count their number of occurrence.<br/>

![lda_example](https://user-images.githubusercontent.com/30851539/62182800-fa89af80-b325-11e9-87f7-50afcd83aee7.png) <br/>
![lda_example_words](https://user-images.githubusercontent.com/30851539/62182807-fd84a000-b325-11e9-9ad9-b9b8cba07be1.png)

Finally, we build the LDA model by choosing the number of topics. Here I made an "ansatz" that there are 40 distinct topics since there are 40 different categories associated to the dataset. Some of the topics are shown as below:<br/>
![lda_topics](https://user-images.githubusercontent.com/30851539/62182495-c8c41900-b324-11e9-832e-036777988e36.png)<br/>
I put the first 9 topics into wordclouds for better visualization. The size of the word is proportionate to its weight/significance in the given sentence.<br/>

![lda40_wordcloud](https://user-images.githubusercontent.com/30851539/62183034-b1862b00-b326-11e9-9f55-58968b39df8d.png)

As we can see, each topic is just a combination of keywords. For the chosen example, its assigned topics are:<br/>
![lda_example](https://user-images.githubusercontent.com/30851539/62182499-ccf03680-b324-11e9-9355-28fc098605be.png)

We can then infer its topic may be "Police shoots and kills black lives".
Here is a great visualization of LDA created by pyLDAvis library. Ideally, the topic bubble should not be overlapping. If the topics are too crowded, it may be an indicator that the number-of-topic parameter is set too high.<br/>

![lda_vis](https://user-images.githubusercontent.com/30851539/62178213-269d3480-b316-11e9-8547-7ba1ada5f74c.gif)

### Keyword Extraction (KE)
1. Using POS tagger
2. Using TextRank
3. Using RAKE

<table border="1" class="dataframe">  <thead>    <tr style="text-align: right;">      <th></th>      <th>italy</th>      <th>aim</th>      <th>to</th>      <th>rattle</th>      <th>england</th>      <th>coach</th>      <th>john</th>      <th>kirwan</th>      <th>believes</th>      <th>his</th>      <th>side</th>      <th>can</th>      <th>upset</th>      <th>as</th>      <th>the</th>      <th>six</th>      <th>nations</th>      <th>wooden</th>      <th>spoon</th>      <th>battle</th>      <th>hots</th>      <th>up</th>      <th>two</th>      <th>sides</th>      <th>both</th>      <th>without</th>      <th>a</th>      <th>win</th>      <th>meet</th>      <th>on</th>      <th>march</th>      <th>at</th>      <th>twickenham</th>      <th>and</th>      <th>says</th>      <th>will</th>      <th>be</th>      <th>hoping</th>      <th>make</th>      <th>most</th>      <th>of</th>      <th>englands</th>      <th>current</th>      <th>slump</th>      <th>we</th>      <th>have</th>      <th>sure</th>      <th>france</th>      <th>games</th>      <th>are</th>      <th>tough</th>      <th>for</th>      <th>them</th>      <th>not</th>      <th>been</th>      <th>having</th>      <th>best</th>      <th>championships</th>      <th>that</th>      <th>is</th>      <th>big</th>      <th>one</th>      <th>us</th>      <th>i</th>      <th>am</th>      <th>my</th>      <th>players</th>      <th>rise</th>      <th>occasion</th>      <th>he</th>      <th>said</th>      <th>but</th>      <th>admits</th>      <th>lot</th>      <th>hard</th>      <th>work</th>      <th>needed</th>      <th>with</th>      <th>kickers</th>      <th>before</th>      <th>trip</th>      <th>london</th>      <th>roland</th>      <th>de</th>      <th>marigny</th>      <th>luciano</th>      <th>orquera</th>      <th>had</th>      <th>miserable</th>      <th>time</th>      <th>boot</th>      <th>in</th>      <th>dire</th>      <th>defeat</th>      <th>scotland</th>      <th>chris</th>      <th>paterson</th>      <th>stole</th>      <th>show</th>      <th>give</th>      <th>hosts</th>      <th>muchneeded</th>      <th>victory</th>      <th>kicking</th>      <th>was</th>      <th>decisive</th>      <th>factor</th>      <th>which</th>      <th>cost</th>      <th>it</th>      <th>could</th>      <th>go</th>      <th>down</th>      <th>again</th>      <th>next</th>      <th>confidence</th>      <th>positive</th>      <th>put</th>      <th>everything</th>      <th>together</th>      <th>against</th>      <th>meanwhile</th>      <th>licking</th>      <th>their</th>      <th>wounds</th>      <th>rueing</th>      <th>what</th>      <th>might</th>      <th>decisions</th>      <th>from</th>      <th>referee</th>      <th>jonathan</th>      <th>kaplan</th>      <th>gone</th>      <th>second</th>      <th>half</th>      <th>dublin</th>      <th>first</th>      <th>mark</th>      <th>cueto</th>      <th>judged</th>      <th>offside</th>      <th>chased</th>      <th>flyhalf</th>      <th>charlie</th>      <th>hodgsons</th>      <th>kick</th>      <th>then</th>      <th>opted</th>      <th>call</th>      <th>upon</th>      <th>video</th>      <th>evidence</th>      <th>see</th>      <th>if</th>      <th>josh</th>      <th>lewsey</th>      <th>touched</th>      <th>after</th>      <th>being</th>      <th>driven</th>      <th>over</th>      <th>irelands</th>      <th>line</th>      <th>centre</th>      <th>jamie</th>      <th>noon</th>      <th>least</th>      <th>showed</th>      <th>better</th>      <th>form</th>      <th>than</th>      <th>previous</th>      <th>defeats</th>      <th>definitely</th>      <th>improved</th>      <th>an</th>      <th>inform</th>      <th>irish</th>      <th>went</th>      <th>quietly</th>      <th>confident</th>      <th>would</th>      <th>able</th>      <th>compete</th>      <th>think</th>      <th>got</th>      <th>now</th>      <th>take</th>      <th>positives</th>      <th>into</th>      <th>game</th>      <th>under</th>      <th>no</th>      <th>illusions</th>      <th>going</th>      <th>easy</th>      <th>need</th>      <th>equalled</th>      <th>year</th>      <th>low</th>      <th>four</th>      <th>successive</th>      <th>championship</th>      <th>including</th>      <th>paris</th>      <th>last</th>      <th>season</th>      <th>lost</th>      <th>row</th>      <th>andy</th>      <th>robinson</th>      <th>predecessor</th>      <th>sir</th>      <th>clive</th>      <th>woodward</th>      <th>began</th>      <th>sevenyear</th>      <th>reign</th>      <th>three</th>      <th>draws</th>    </tr>  </thead>  <tbody>    <tr>      <th>Tags</th>      <td>JJ</td>      <td>NN</td>      <td>TO</td>      <td>VB</td>      <td>NN</td>      <td>NN</td>      <td>NN</td>      <td>NN</td>      <td>VBZ</td>      <td>PRP$</td>      <td>NN</td>      <td>MD</td>      <td>VB</td>      <td>IN</td>      <td>DT</td>      <td>CD</td>      <td>NNS</td>      <td>VBP</td>      <td>JJ</td>      <td>NN</td>      <td>VBD</td>      <td>RP</td>      <td>CD</td>      <td>NNS</td>      <td>DT</td>      <td>IN</td>      <td>DT</td>      <td>NN</td>      <td>NN</td>      <td>IN</td>      <td>NN</td>      <td>IN</td>      <td>NN</td>      <td>CC</td>      <td>VBZ</td>      <td>MD</td>      <td>VB</td>      <td>VBG</td>      <td>VB</td>      <td>JJS</td>      <td>IN</td>      <td>NNS</td>      <td>JJ</td>      <td>NN</td>      <td>PRP</td>      <td>VBP</td>      <td>JJ</td>      <td>NN</td>      <td>NNS</td>      <td>VBP</td>      <td>JJ</td>      <td>IN</td>      <td>PRP</td>      <td>RB</td>      <td>VBN</td>      <td>VBG</td>      <td>JJS</td>      <td>NNS</td>      <td>IN</td>      <td>VBZ</td>      <td>JJ</td>      <td>NN</td>      <td>PRP</td>      <td>VB</td>      <td>VBP</td>      <td>PRP$</td>      <td>NNS</td>      <td>VB</td>      <td>NN</td>      <td>PRP</td>      <td>VBD</td>      <td>CC</td>      <td>NNS</td>      <td>NN</td>      <td>JJ</td>      <td>NN</td>      <td>VBN</td>      <td>IN</td>      <td>NNS</td>      <td>IN</td>      <td>NN</td>      <td>VB</td>      <td>NN</td>      <td>IN</td>      <td>FW</td>      <td>VB</td>      <td>NN</td>      <td>VBD</td>      <td>JJ</td>      <td>NN</td>      <td>NN</td>      <td>IN</td>      <td>JJ</td>      <td>NN</td>      <td>NN</td>      <td>JJ</td>      <td>NN</td>      <td>VBD</td>      <td>NN</td>      <td>VB</td>      <td>NNS</td>      <td>JJ</td>      <td>NN</td>      <td>VBG</td>      <td>VBD</td>      <td>JJ</td>      <td>NN</td>      <td>WDT</td>      <td>VBP</td>      <td>PRP</td>      <td>MD</td>      <td>VB</td>      <td>RB</td>      <td>RB</td>      <td>JJ</td>      <td>NN</td>      <td>JJ</td>      <td>VB</td>      <td>NN</td>      <td>RB</td>      <td>IN</td>      <td>NN</td>      <td>VBG</td>      <td>PRP$</td>      <td>NNS</td>      <td>VBG</td>      <td>WP</td>      <td>MD</td>      <td>NNS</td>      <td>IN</td>      <td>JJ</td>      <td>NN</td>      <td>VB</td>      <td>VBN</td>      <td>JJ</td>      <td>NN</td>      <td>VB</td>      <td>RB</td>      <td>JJ</td>      <td>NN</td>      <td>VBN</td>      <td>RB</td>      <td>VBD</td>      <td>JJ</td>      <td>JJ</td>      <td>NNS</td>      <td>VBP</td>      <td>RB</td>      <td>VBD</td>      <td>VB</td>      <td>IN</td>      <td>JJ</td>      <td>NN</td>      <td>VB</td>      <td>IN</td>      <td>JJ</td>      <td>NN</td>      <td>VBN</td>      <td>IN</td>      <td>VBG</td>      <td>VBN</td>      <td>IN</td>      <td>NNS</td>      <td>NN</td>      <td>NN</td>      <td>NN</td>      <td>NN</td>      <td>JJS</td>      <td>VBD</td>      <td>JJR</td>      <td>NN</td>      <td>IN</td>      <td>JJ</td>      <td>NNS</td>      <td>RB</td>      <td>VBN</td>      <td>DT</td>      <td>JJ</td>      <td>JJ</td>      <td>VBD</td>      <td>RB</td>      <td>JJ</td>      <td>MD</td>      <td>JJ</td>      <td>VB</td>      <td>VBP</td>      <td>VBN</td>      <td>RB</td>      <td>VBP</td>      <td>VBZ</td>      <td>IN</td>      <td>NN</td>      <td>IN</td>      <td>DT</td>      <td>NNS</td>      <td>VBG</td>      <td>JJ</td>      <td>VBP</td>      <td>VBN</td>      <td>NN</td>      <td>NN</td>      <td>CD</td>      <td>JJ</td>      <td>NN</td>      <td>VBG</td>      <td>NN</td>      <td>JJ</td>      <td>NN</td>      <td>VBN</td>      <td>NN</td>      <td>JJ</td>      <td>NN</td>      <td>NN</td>      <td>NN</td>      <td>JJ</td>      <td>NN</td>      <td>VBD</td>      <td>JJ</td>      <td>NN</td>      <td>CD</td>      <td>NNS</td>    </tr>  </tbody></table>

<br/>
**Extracted keywords and tags**
<table border="1" class="dataframe">  <thead>    <tr style="text-align: right;">      <th></th>      <th>aim</th>      <th>england</th>      <th>coach</th>      <th>john</th>      <th>kirwan</th>      <th>side</th>      <th>battle</th>      <th>meet</th>      <th>march</th>      <th>twickenham</th>      <th>slump</th>      <th>france</th>      <th>one</th>      <th>occasion</th>      <th>lot</th>      <th>work</th>      <th>trip</th>      <th>roland</th>      <th>orquera</th>      <th>time</th>      <th>boot</th>      <th>defeat</th>      <th>paterson</th>      <th>show</th>      <th>victory</th>      <th>kicking</th>      <th>factor</th>      <th>scotland</th>      <th>confidence</th>      <th>i</th>      <th>everything</th>      <th>meanwhile</th>      <th>jonathan</th>      <th>kaplan</th>      <th>half</th>      <th>dublin</th>      <th>cueto</th>      <th>evidence</th>      <th>lewsey</th>      <th>line</th>      <th>centre</th>      <th>jamie</th>      <th>noon</th>      <th>form</th>      <th>game</th>      <th>win</th>      <th>year</th>      <th>low</th>      <th>championship</th>      <th>paris</th>      <th>season</th>      <th>row</th>      <th>robinson</th>      <th>predecessor</th>      <th>sir</th>      <th>woodward</th>      <th>reign</th>    </tr>  </thead>  <tbody>    <tr>      <th>Tags</th>      <td>NN</td>      <td>NN</td>      <td>NN</td>      <td>NN</td>      <td>NN</td>      <td>NN</td>      <td>NN</td>      <td>NN</td>      <td>NN</td>      <td>NN</td>      <td>NN</td>      <td>NN</td>      <td>NN</td>      <td>NN</td>      <td>NN</td>      <td>NN</td>      <td>NN</td>      <td>NN</td>      <td>NN</td>      <td>NN</td>      <td>NN</td>      <td>NN</td>      <td>NN</td>      <td>NN</td>      <td>NN</td>      <td>NN</td>      <td>NN</td>      <td>NN</td>      <td>NN</td>      <td>NN</td>      <td>NN</td>      <td>NN</td>      <td>NN</td>      <td>NN</td>      <td>NN</td>      <td>NN</td>      <td>NN</td>      <td>NN</td>      <td>NN</td>      <td>NN</td>      <td>NN</td>      <td>NN</td>      <td>NN</td>      <td>NN</td>      <td>NN</td>      <td>NN</td>      <td>NN</td>      <td>NN</td>      <td>NN</td>      <td>NN</td>      <td>NN</td>      <td>NN</td>      <td>NN</td>      <td>NN</td>      <td>NN</td>      <td>NN</td>      <td>NN</td>    </tr>  </tbody></table>


### Event Extraction (EE)
EE gathers knowledge about periodical incidents found in texts, automatically identifying information about what happed and when it happened. The amount of text generated daily are enormous. Being able to extract key information from a giant pool of data can help us be more efficient. For example, extracting events from business news aids users to perceive market trends, stay up to date with competitors' strategies and to make valuable investment decisioins.
