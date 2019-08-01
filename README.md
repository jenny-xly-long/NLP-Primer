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

### Keyword Extraction (KE)
Keyword extraction is an important task in information extraction. It automatically identifies terms that have the most significance or best describes the text. Multiple techniques can be used to extract keywords, one of the most straight forward way to do so is to use Term Frequency - Inverse Document Frequency (TF-IDF). This method is quite intuitive in the sense that it scores the importance of a word by considering its number of occurrence in the given document/sentence and in the entire corpus of documents/sentences. Naturally, if a word occurs frequently in one document, it has high weight/importance; if a word occurs in all document, it is considered as a generic word, thus less important. Here I will present three other ways to perform the task.

#### 1. Using POS tagging and chunking
We can use POS tagger to extract keywords. Given the following example:<br/>
```When former San Francisco 49ers quarterback Colin Kaepernick took a knee during the national anthem in August 2016, it was in protest of unjust police killings of black Americans.For his courage, Kaepernick lost his job, the NFL lost its mind by forbidding the peaceful action ― and meanwhile, at least 378 black Americans have lost their lives in police killings. That most recent estimate of black police violence victims comes from data compiled by The Washington Post and analyzed by HuffPost.Last August, HuffPost reported that based on the Post’s data, at least 223 black Americans had been killed by police gunfire in the year since Kaepernick first sat, then took a knee, to protest police violence. Less than a year later, that number has increased by at least 155 people.```

After preprocessing, use NLTK POS-tagger tool to generate the follwoing word-tag pairs:
<table border="1" class="dataframe">  <thead>    <tr style="text-align: right;">      <th></th>      <th>When</th>      <th>former</th>      <th>San</th>      <th>Francisco</th>      <th>49ers</th>      <th>quarterback</th>      <th>Colin</th>      <th>Kaepernick</th>      <th>took</th>      <th>knee</th>      <th>national</th>      <th>anthem</th>      <th>August</th>      <th>2016</th>      <th>protest</th>      <th>unjust</th>      <th>police</th>      <th>killings</th>      <th>black</th>      <th>Americans</th>      <th>For</th>      <th>courage</th>      <th>lost</th>      <th>job</th>      <th>NFL</th>      <th>mind</th>      <th>forbidding</th>      <th>peaceful</th>      <th>action</th>      <th>meanwhile</th>      <th>least</th>      <th>378</th>      <th>lives</th>      <th>That</th>      <th>recent</th>      <th>estimate</th>      <th>violence</th>      <th>victims</th>      <th>comes</th>      <th>data</th>      <th>compiled</th>      <th>The</th>      <th>Washington</th>      <th>Post</th>      <th>analyzed</th>      <th>HuffPost</th>      <th>Last</th>      <th>reported</th>      <th>based</th>      <th>223</th>      <th>killed</th>      <th>gunfire</th>      <th>year</th>      <th>since</th>      <th>first</th>      <th>sat</th>      <th>Less</th>      <th>later</th>      <th>number</th>      <th>increased</th>      <th>155</th>      <th>people</th>    </tr>  </thead>  <tbody>    <tr>      <th>Tags</th>      <td>WRB</td>      <td>JJ</td>      <td>NNP</td>      <td>NNP</td>      <td>CD</td>      <td>NN</td>      <td>NNP</td>      <td>NNP</td>      <td>VBD</td>      <td>NN</td>      <td>JJ</td>      <td>NN</td>      <td>NNP</td>      <td>CD</td>      <td>NN</td>      <td>JJ</td>      <td>NN</td>      <td>NNS</td>      <td>JJ</td>      <td>NNPS</td>      <td>IN</td>      <td>NN</td>      <td>VBN</td>      <td>NN</td>      <td>NNP</td>      <td>NN</td>      <td>VBG</td>      <td>JJ</td>      <td>NN</td>      <td>RB</td>      <td>JJS</td>      <td>CD</td>      <td>NNS</td>      <td>WDT</td>      <td>JJ</td>      <td>NN</td>      <td>NN</td>      <td>NNS</td>      <td>VBZ</td>      <td>NNS</td>      <td>VBD</td>      <td>DT</td>      <td>NNP</td>      <td>NNP</td>      <td>VBD</td>      <td>NNP</td>      <td>JJ</td>      <td>VBD</td>      <td>VBN</td>      <td>CD</td>      <td>VBN</td>      <td>NN</td>      <td>NN</td>      <td>IN</td>      <td>RB</td>      <td>VBD</td>      <td>NNP</td>      <td>RB</td>      <td>NN</td>      <td>VBD</td>      <td>CD</td>      <td>NNS</td>    </tr>  </tbody></table>
<br/>

Now let's perform name entity (NE) chunking to add more structure/name entity tags to the sentences. The NE-chunk classifier is supposed to recognize PERSON, ORGANISATION, etc. Here are the top level tags and their meaning:<br/>
> - geo = Geographical Entity
> - org = Organization
> - per = Person
> - gpe = Geopolitical Entity
> - tim = Time indicator
> - art = Artifact
> - eve = Event
> - nat = Natural Phenomenon
<br/>
<table border="1" class="dataframe">  <thead>    <tr style="text-align: right;">      <th></th>      <th>0</th>      <th>1</th>      <th>2</th>      <th>3</th>      <th>4</th>      <th>5</th>      <th>6</th>      <th>7</th>      <th>8</th>      <th>9</th>      <th>10</th>      <th>11</th>      <th>12</th>      <th>13</th>      <th>14</th>      <th>15</th>      <th>16</th>      <th>17</th>      <th>18</th>      <th>19</th>      <th>20</th>      <th>21</th>      <th>22</th>      <th>23</th>      <th>24</th>      <th>25</th>      <th>26</th>      <th>27</th>      <th>28</th>      <th>29</th>      <th>30</th>      <th>31</th>      <th>32</th>      <th>33</th>      <th>34</th>      <th>35</th>      <th>36</th>      <th>37</th>      <th>38</th>      <th>39</th>      <th>40</th>      <th>41</th>      <th>42</th>      <th>43</th>      <th>44</th>      <th>45</th>      <th>46</th>      <th>47</th>      <th>48</th>      <th>49</th>      <th>50</th>      <th>51</th>      <th>52</th>      <th>53</th>      <th>54</th>      <th>55</th>      <th>56</th>      <th>57</th>      <th>58</th>      <th>59</th>      <th>60</th>      <th>61</th>      <th>62</th>      <th>63</th>      <th>64</th>      <th>65</th>      <th>66</th>      <th>67</th>      <th>68</th>      <th>69</th>      <th>70</th>      <th>71</th>      <th>72</th>      <th>73</th>      <th>74</th>      <th>75</th>      <th>76</th>      <th>77</th>      <th>78</th>      <th>79</th>      <th>80</th>      <th>81</th>      <th>82</th>      <th>83</th>      <th>84</th>      <th>85</th>      <th>86</th>    </tr>  </thead>  <tbody>    <tr>      <th>Words</th>      <td>When</td>      <td>former</td>      <td>San</td>      <td>Francisco</td>      <td>49ers</td>      <td>quarterback</td>      <td>Colin</td>      <td>Kaepernick</td>      <td>took</td>      <td>knee</td>      <td>national</td>      <td>anthem</td>      <td>August</td>      <td>2016</td>      <td>protest</td>      <td>unjust</td>      <td>police</td>      <td>killings</td>      <td>black</td>      <td>Americans</td>      <td>For</td>      <td>courage</td>      <td>Kaepernick</td>      <td>lost</td>      <td>job</td>      <td>NFL</td>      <td>lost</td>      <td>mind</td>      <td>forbidding</td>      <td>peaceful</td>      <td>action</td>      <td>meanwhile</td>      <td>least</td>      <td>378</td>      <td>black</td>      <td>Americans</td>      <td>lost</td>      <td>lives</td>      <td>police</td>      <td>killings</td>      <td>That</td>      <td>recent</td>      <td>estimate</td>      <td>black</td>      <td>police</td>      <td>violence</td>      <td>victims</td>      <td>comes</td>      <td>data</td>      <td>compiled</td>      <td>The</td>      <td>Washington</td>      <td>Post</td>      <td>analyzed</td>      <td>HuffPost</td>      <td>Last</td>      <td>August</td>      <td>HuffPost</td>      <td>reported</td>      <td>based</td>      <td>Post</td>      <td>data</td>      <td>least</td>      <td>223</td>      <td>black</td>      <td>Americans</td>      <td>killed</td>      <td>police</td>      <td>gunfire</td>      <td>year</td>      <td>since</td>      <td>Kaepernick</td>      <td>first</td>      <td>sat</td>      <td>took</td>      <td>knee</td>      <td>protest</td>      <td>police</td>      <td>violence</td>      <td>Less</td>      <td>year</td>      <td>later</td>      <td>number</td>      <td>increased</td>      <td>least</td>      <td>155</td>      <td>people</td>    </tr>    <tr>      <th>POS Tags</th>      <td>WRB</td>      <td>JJ</td>      <td>NNP</td>      <td>NNP</td>      <td>CD</td>      <td>NN</td>      <td>NNP</td>      <td>NNP</td>      <td>VBD</td>      <td>NNP</td>      <td>JJ</td>      <td>NN</td>      <td>NNP</td>      <td>CD</td>      <td>NN</td>      <td>JJ</td>      <td>NN</td>      <td>NNS</td>      <td>JJ</td>      <td>NNPS</td>      <td>IN</td>      <td>NN</td>      <td>NNP</td>      <td>VBD</td>      <td>NN</td>      <td>NNP</td>      <td>VBD</td>      <td>NN</td>      <td>VBG</td>      <td>JJ</td>      <td>NN</td>      <td>RB</td>      <td>JJS</td>      <td>CD</td>      <td>JJ</td>      <td>NNPS</td>      <td>VBN</td>      <td>NNS</td>      <td>JJ</td>      <td>NNS</td>      <td>WDT</td>      <td>JJ</td>      <td>NN</td>      <td>JJ</td>      <td>NN</td>      <td>NN</td>      <td>NNS</td>      <td>VBZ</td>      <td>NNS</td>      <td>VBD</td>      <td>DT</td>      <td>NNP</td>      <td>NNP</td>      <td>VBD</td>      <td>NNP</td>      <td>JJ</td>      <td>NNP</td>      <td>NNP</td>      <td>VBD</td>      <td>VBN</td>      <td>NNP</td>      <td>NNS</td>      <td>JJS</td>      <td>CD</td>      <td>JJ</td>      <td>NNPS</td>      <td>VBN</td>      <td>NN</td>      <td>NN</td>      <td>NN</td>      <td>IN</td>      <td>NNP</td>      <td>RB</td>      <td>VBD</td>      <td>VBD</td>      <td>NN</td>      <td>NN</td>      <td>NN</td>      <td>NN</td>      <td>NNP</td>      <td>NN</td>      <td>RB</td>      <td>NN</td>      <td>VBD</td>      <td>JJS</td>      <td>CD</td>      <td>NNS</td>    </tr>    <tr>      <th>IOB Tags</th>      <td>O</td>      <td>O</td>      <td>B-GPE</td>      <td>O</td>      <td>O</td>      <td>O</td>      <td>B-PERSON</td>      <td>I-PERSON</td>      <td>O</td>      <td>O</td>      <td>O</td>      <td>O</td>      <td>O</td>      <td>O</td>      <td>O</td>      <td>O</td>      <td>O</td>      <td>O</td>      <td>O</td>      <td>O</td>      <td>O</td>      <td>O</td>      <td>B-PERSON</td>      <td>O</td>      <td>O</td>      <td>B-ORGANIZATION</td>      <td>O</td>      <td>O</td>      <td>O</td>      <td>O</td>      <td>O</td>      <td>O</td>      <td>O</td>      <td>O</td>      <td>O</td>      <td>O</td>      <td>O</td>      <td>O</td>      <td>O</td>      <td>O</td>      <td>O</td>      <td>O</td>      <td>O</td>      <td>O</td>      <td>O</td>      <td>O</td>      <td>O</td>      <td>O</td>      <td>O</td>      <td>O</td>      <td>O</td>      <td>B-ORGANIZATION</td>      <td>I-ORGANIZATION</td>      <td>O</td>      <td>B-ORGANIZATION</td>      <td>O</td>      <td>O</td>      <td>B-ORGANIZATION</td>      <td>O</td>      <td>O</td>      <td>B-ORGANIZATION</td>      <td>O</td>      <td>O</td>      <td>O</td>      <td>O</td>      <td>O</td>      <td>O</td>      <td>O</td>      <td>O</td>      <td>O</td>      <td>O</td>      <td>B-PERSON</td>      <td>O</td>      <td>O</td>      <td>O</td>      <td>O</td>      <td>O</td>      <td>O</td>      <td>O</td>      <td>B-PERSON</td>      <td>O</td>      <td>O</td>      <td>O</td>      <td>O</td>      <td>O</td>      <td>O</td>      <td>O</td>    </tr>  </tbody></table>
<br/>
As seen in the "IOB Tag" row, the tagger mostly successfully picked up different name entities in the given text. We can then extract those with the NE tags as keywords. Using SpaCy's displacy visualization library, we get the following graph:

![tagged_sentence](https://user-images.githubusercontent.com/30851539/62237415-e6ce5f80-b39e-11e9-8d78-d729bb03d219.gif)


#### 2. Using TextRank
TextRank is a graph-based ranking model for text processing, especially for keyword and sentence extraction (Rada and Tarau, 2004). This methode is similar to Google's PageRank algorithm (Brin and Page, 1998). Intuitively, TextRank works well because it does not only rely on the local context of a text unit, but it takes into account information recursively drawn from the entire text. It is able to identify connections between various entities in a text and implements the concept of recommendation.
<br/>

TextRank can be implemented through Python's *summa* libray. For example, we take the same text as before and we get the following keywords:
<table border="1" class="dataframe">  <thead>    <tr style="text-align: right;">      <th></th>      <th>0</th>      <th>1</th>      <th>2</th>      <th>3</th>      <th>4</th>      <th>5</th>      <th>6</th>      <th>7</th>    </tr>  </thead>  <tbody>    <tr>      <th>Keywords</th>      <td>police</td>      <td>lost</td>      <td>post</td>      <td>kaepernick took</td>      <td>black</td>      <td>protest</td>      <td>data</td>      <td>huffpost</td>    </tr>  </tbody></table>
<br/>

Building on to of the TextRank idea, we can illustrate a keywords-relation graph using Liu's implementation (https://github.com/liuhuanyong/TextGrapher). The above text example result in the following text graph.
![keyword_graph](https://user-images.githubusercontent.com/30851539/62246646-15096a80-b3b2-11e9-87e7-7781535f6929.gif)

#### 3. Unsupervised





### Topic Modeling
Topic modeling is an unsupervised technique to discover topics across various text documents. It has various applications in different domain. For instance, historians can use it to identify important events in history; web based libraries can use it to recommend books based on your past readings. News providers can leverage the technique to understand articles quickly or to group similar articles.

#### 1. Latent Semantic Analysis (LSA)
#### 2. Latent Dirichlet Allocation (LDA)
LDA is a Bayesian model that uses Dirichlet priors to compute document-topic and word-topic distributions. It has two basic assumptions: 
```
1. Each document consists of a mixture of topics
2. Each topic consists of a set of words
```
LDA considers each document as a collection of topics of different weights. And each topic as a collection of keywords in a certain proportion. Therefore, from LDA's perspective, a topic is nothing but a collection of representative, dominant keywords. You can then infer the topic by looking at the collection of keywords. <br/>

**Logic of LDA:**
<code><pre>1. Specify the number of topics *N* to discover (note that this is a hyperparameter of the model that we need to fine tune)
2. Randomly assign each word of the documents to one the the *N* topics.
3. Compute the product of P(Topic *T* | Document *D*) [probability of documents *D* assigned to topic *T*] and P(Word *w* | Topic *T*)[probability of topic *T* assignment contributed by word *w*].
4. Re-assign a new topic to each word according to the above result which represents the likelihood that topic *T* would generate word *w*.
5. Repeat steps 3 and 4 until we reach a steady state where topics are assigned correctly according to the computed probability.</code></pre>

**Example of LDA implementation:**
LDA can be implemented using Sklean or gensim library. I am using gensim and wordnet on the News Category(attach link) dataset. Please see "lda.py" for detailed code. The goal here is to further understand LDA through some code and visualization.

Here is a snapshot of the data set<br/>

<table border="1" class="dataframe">  <thead>    <tr style="text-align: right;">      <th></th>      <th>category</th>      <th>headline</th>      <th>index</th>    </tr>  </thead>  <tbody>    <tr>      <th>0</th>      <td>CRIME</td>      <td>There Were 2 Mass Shootings In Texas Last Week...</td>      <td>0</td>    </tr>    <tr>      <th>1</th>      <td>ENTERTAINMENT</td>      <td>Will Smith Joins Diplo And Nicky Jam For The 2...</td>      <td>1</td>    </tr>    <tr>      <th>2</th>      <td>ENTERTAINMENT</td>      <td>Hugh Grant Marries For The First Time At Age 57</td>      <td>2</td>    </tr>    <tr>      <th>3</th>      <td>ENTERTAINMENT</td>      <td>Jim Carrey Blasts \'Castrato\' Adam Schiff And D...</td>      <td>3</td>    </tr>    <tr>      <th>4</th>      <td>ENTERTAINMENT</td>      <td>Julianna Margulies Uses Donald Trump Poop Bags...</td>      <td>4</td>    </tr>    <tr>      <th>5</th>      <td>ENTERTAINMENT</td>      <td>Morgan Freeman \'Devastated\' That Sexual Harass...</td>      <td>5</td>    </tr>    <tr>      <th>6</th>      <td>ENTERTAINMENT</td>      <td>Donald Trump Is Lovin\' New McDonald\'s Jingle I...</td>      <td>6</td>    </tr>    <tr>      <th>7</th>      <td>ENTERTAINMENT</td>      <td>What To Watch On Amazon Prime That’s New This ...</td>      <td>7</td>    </tr>    <tr>      <th>8</th>      <td>ENTERTAINMENT</td>      <td>Mike Myers Reveals He\'d \'Like To\' Do A Fourth ...</td>      <td>8</td>    </tr>    <tr>      <th>9</th>      <td>ENTERTAINMENT</td>      <td>What To Watch On Hulu That’s New This Week</td>      <td>9</td>    </tr>  </tbody></table>


We first preprocess the data by removing the stopwords, tokenizing, lemmatizig and stemming the text.<br/>
<table border="1" class="dataframe">  <thead>    <tr style="text-align: right;">      <th></th>      <th>headline</th>    </tr>  </thead>  <tbody>    <tr>      <th>0</th>      <td>[mass, shoot, texa, week]</td>    </tr>    <tr>      <th>1</th>      <td>[smith, join, diplo, nicki, world, offici, song]</td>    </tr>    <tr>      <th>2</th>      <td>[hugh, grant, marri, time]</td>    </tr>    <tr>      <th>3</th>      <td>[carrey, blast, castrato, adam, schiff, democr...</td>    </tr>    <tr>      <th>4</th>      <td>[julianna, marguli, use, donald, trump, poop, ...</td>    </tr>    <tr>      <th>5</th>      <td>[morgan, freeman, devast, sexual, harass, clai...</td>    </tr>    <tr>      <th>6</th>      <td>[donald, trump, lovin, mcdonald, jingl, tonight]</td>    </tr>    <tr>      <th>7</th>      <td>[watch, amazon, prime, week]</td>    </tr>    <tr>      <th>8</th>      <td>[mike, myer, reveal, like, fourth, austin, pow...</td>    </tr>    <tr>      <th>9</th>      <td>[watch, hulu, week]</td>    </tr>  </tbody></table>

We then match each of the words to a word ID and store them in a dictionary, shown as following<br/>
<table border="1" class="dataframe">  <thead>    <tr style="text-align: right;">      <th></th>      <th>0</th>      <th>1</th>      <th>2</th>      <th>3</th>      <th>4</th>      <th>5</th>      <th>6</th>      <th>7</th>      <th>8</th>      <th>9</th>      <th>10</th>      <th>11</th>      <th>12</th>      <th>13</th>      <th>14</th>      <th>15</th>      <th>16</th>      <th>17</th>      <th>18</th>      <th>19</th>      <th>20</th>      <th>21</th>      <th>22</th>      <th>23</th>      <th>24</th>      <th>25</th>      <th>26</th>      <th>27</th>      <th>28</th>      <th>29</th>      <th>30</th>      <th>31</th>      <th>32</th>      <th>33</th>      <th>34</th>      <th>35</th>      <th>36</th>      <th>37</th>      <th>38</th>      <th>39</th>      <th>40</th>      <th>41</th>      <th>42</th>      <th>43</th>      <th>44</th>      <th>45</th>      <th>46</th>      <th>47</th>      <th>48</th>      <th>49</th>      <th>50</th>      <th>51</th>      <th>52</th>      <th>53</th>      <th>54</th>      <th>55</th>      <th>56</th>      <th>57</th>      <th>58</th>      <th>59</th>      <th>60</th>      <th>61</th>      <th>62</th>      <th>63</th>      <th>64</th>      <th>65</th>      <th>66</th>      <th>67</th>      <th>68</th>      <th>69</th>      <th>70</th>      <th>71</th>      <th>72</th>      <th>73</th>      <th>74</th>      <th>75</th>      <th>76</th>      <th>77</th>      <th>78</th>      <th>79</th>      <th>80</th>      <th>81</th>      <th>82</th>      <th>83</th>      <th>84</th>      <th>85</th>      <th>86</th>      <th>87</th>      <th>88</th>      <th>89</th>      <th>90</th>      <th>91</th>      <th>92</th>      <th>93</th>      <th>94</th>      <th>95</th>      <th>96</th>      <th>97</th>      <th>98</th>      <th>99</th>    </tr>  </thead>  <tbody>    <tr>      <th>Words</th>      <td>mass</td>      <td>shoot</td>      <td>texa</td>      <td>week</td>      <td>diplo</td>      <td>join</td>      <td>nicki</td>      <td>offici</td>      <td>smith</td>      <td>song</td>      <td>world</td>      <td>grant</td>      <td>hugh</td>      <td>marri</td>      <td>time</td>      <td>adam</td>      <td>artwork</td>      <td>blast</td>      <td>carrey</td>      <td>castrato</td>      <td>democrat</td>      <td>schiff</td>      <td>bag</td>      <td>donald</td>      <td>julianna</td>      <td>marguli</td>      <td>pick</td>      <td>poop</td>      <td>trump</td>      <td>use</td>      <td>claim</td>      <td>devast</td>      <td>freeman</td>      <td>harass</td>      <td>legaci</td>      <td>morgan</td>      <td>sexual</td>      <td>undermin</td>      <td>jingl</td>      <td>lovin</td>      <td>mcdonald</td>      <td>tonight</td>      <td>amazon</td>      <td>prime</td>      <td>watch</td>      <td>austin</td>      <td>film</td>      <td>fourth</td>      <td>like</td>      <td>mike</td>      <td>myer</td>      <td>power</td>      <td>reveal</td>      <td>hulu</td>      <td>justin</td>      <td>school</td>      <td>timberlak</td>      <td>victim</td>      <td>visit</td>      <td>jong</td>      <td>korea</td>      <td>korean</td>      <td>meet</td>      <td>north</td>      <td>presid</td>      <td>south</td>      <td>summit</td>      <td>talk</td>      <td>call</td>      <td>grow</td>      <td>life</td>      <td>oyster</td>      <td>region</td>      <td>remot</td>      <td>risk</td>      <td>robot</td>      <td>crackdown</td>      <td>immigr</td>      <td>kid</td>      <td>parent</td>      <td>put</td>      <td>strain</td>      <td>alli</td>      <td>concern</td>      <td>obtain</td>      <td>putin</td>      <td>wiretap</td>      <td>edward</td>      <td>love</td>      <td>snowden</td>      <td>vladimir</td>      <td>booyah</td>      <td>hilari</td>      <td>obama</td>      <td>photograph</td>      <td>troll</td>      <td>abort</td>      <td>amend</td>      <td>ireland</td>      <td>landslid</td>    </tr>  </tbody></table>

Here is one example from the data set, we can see if any of the words in the dictionary occured in this sentence and we can count their number of occurrence.<br/>
```Police killed at least 378 black Americans from the moment Colin Kaepernick protested```
<br/>
> Word 149 ("protest") appears 1 time.<br/>
> Word 157 ("american") appears 1 time.<br/>
> Word 158 ("black") appears 1 time.<br/>
> Word 159 ("colin") appears 1 time.<br/>
> Word 160 ("kaepernick") appears 1 time.<br/>
> Word 161 ("kill") appears 1 time.<br/>
> Word 162 ("moment") appears 1 time.<br/>
> Word 163 ("polic") appears 1 time.

Finally, we build the LDA model by choosing the number of topics. Here I made an "ansatz" that there are 40 distinct topics since there are 40 different categories associated to the dataset. Some of the topics are shown as below:<br/>
<table border="1" class="dataframe">  <thead>    <tr style="text-align: right;">      <th></th>      <th>0</th>      <th>1</th>      <th>2</th>      <th>3</th>      <th>4</th>      <th>5</th>      <th>6</th>      <th>7</th>      <th>8</th>      <th>9</th>      <th>10</th>      <th>11</th>      <th>12</th>      <th>13</th>      <th>14</th>      <th>15</th>      <th>16</th>      <th>17</th>      <th>18</th>      <th>19</th>      <th>20</th>      <th>21</th>      <th>22</th>      <th>23</th>      <th>24</th>      <th>25</th>      <th>26</th>      <th>27</th>      <th>28</th>      <th>29</th>      <th>30</th>      <th>31</th>      <th>32</th>      <th>33</th>      <th>34</th>      <th>35</th>      <th>36</th>      <th>37</th>      <th>38</th>      <th>39</th>    </tr>  </thead>  <tbody>    <tr>      <th>Topics</th>      <td>0.157*"week" + 0.064*"photo" + 0.060*"summer" ...</td>      <td>0.109*"style" + 0.059*"photo" + 0.029*"teen" +...</td>      <td>0.075*"babi" + 0.057*"fall" + 0.057*"photo" + ...</td>      <td>0.069*"right" + 0.041*"feel" + 0.030*"light" +...</td>      <td>0.060*"lose" + 0.045*"heart" + 0.033*"mind" + ...</td>      <td>0.070*"beauti" + 0.069*"star" + 0.060*"photo" ...</td>      <td>0.083*"photo" + 0.034*"cover" + 0.032*"post" +...</td>      <td>0.049*"photo" + 0.038*"bodi" + 0.022*"danger" ...</td>      <td>0.174*"wed" + 0.037*"video" + 0.024*"photo" + ...</td>      <td>0.094*"fashion" + 0.093*"studi" + 0.054*"chang...</td>      <td>0.078*"photo" + 0.074*"parent" + 0.068*"dress"...</td>      <td>0.047*"plan" + 0.042*"parti" + 0.041*"super" +...</td>      <td>0.100*"life" + 0.040*"learn" + 0.037*"real" + ...</td>      <td>0.036*"cook" + 0.034*"workout" + 0.032*"challe...</td>      <td>0.061*"healthi" + 0.057*"secret" + 0.042*"vale...</td>      <td>0.095*"travel" + 0.032*"propos" + 0.031*"olymp...</td>      <td>0.130*"food" + 0.056*"coupl" + 0.037*"mean" + ...</td>      <td>0.097*"health" + 0.049*"hair" + 0.044*"care" +...</td>      <td>0.096*"sleep" + 0.028*"doctor" + 0.027*"name" ...</td>      <td>0.076*"marriag" + 0.045*"child" + 0.035*"date"...</td>      <td>0.103*"kid" + 0.050*"guid" + 0.048*"inspir" + ...</td>      <td>0.055*"children" + 0.041*"money" + 0.029*"film...</td>      <td>0.032*"histori" + 0.029*"self" + 0.027*"makeup...</td>      <td>0.044*"daughter" + 0.038*"street" + 0.031*"wal...</td>      <td>0.054*"girl" + 0.049*"holiday" + 0.041*"video"...</td>      <td>0.109*"way" + 0.063*"cancer" + 0.053*"design" ...</td>      <td>0.067*"citi" + 0.052*"worst" + 0.039*"york" + ...</td>      <td>0.057*"better" + 0.038*"link" + 0.031*"deal" +...</td>      <td>0.204*"best" + 0.041*"photo" + 0.029*"person" ...</td>      <td>0.128*"divorc" + 0.040*"model" + 0.034*"weeken...</td>      <td>0.066*"poll" + 0.051*"save" + 0.035*"question"...</td>      <td>0.093*"thing" + 0.080*"know" + 0.079*"need" + ...</td>      <td>0.060*"open" + 0.058*"great" + 0.037*"pound" +...</td>      <td>0.089*"work" + 0.061*"weight" + 0.039*"loss" +...</td>      <td>0.078*"tip" + 0.048*"photo" + 0.040*"spring" +...</td>      <td>0.042*"power" + 0.041*"favorit" + 0.038*"yoga"...</td>      <td>0.085*"recip" + 0.053*"photo" + 0.053*"america...</td>      <td>0.055*"school" + 0.050*"black" + 0.037*"high" ...</td>      <td>0.064*"idea" + 0.041*"marri" + 0.031*"vintag" ...</td>      <td>0.055*"stop" + 0.030*"suggest" + 0.024*"spot" ...</td>    </tr>  </tbody></table>

I put the first 9 topics into wordclouds for better visualization. The size of the word is proportionate to its weight/significance in the given sentence.<br/>

![lda40_wordcloud](https://user-images.githubusercontent.com/30851539/62183034-b1862b00-b326-11e9-9f55-58968b39df8d.png)

As we can see, each topic is just a combination of keywords. For the chosen example, its assigned topics are:<br/>
![lda_example](https://user-images.githubusercontent.com/30851539/62182499-ccf03680-b324-11e9-9355-28fc098605be.png)

We can then infer its topic may be "Police shoots and kills black lives".
Here is a great visualization of LDA created by pyLDAvis library. Ideally, the topic bubble should not be overlapping. If the topics are too crowded, it may be an indicator that the number-of-topic parameter is set too high.<br/>

![lda_vis](https://user-images.githubusercontent.com/30851539/62246841-82b59680-b3b2-11e9-9d9d-1d59d25a94c7.gif)


### Event Extraction (EE)
EE gathers knowledge about periodical incidents found in texts, automatically identifying information about what happed and when it happened. The amount of text generated daily are enormous. Being able to extract key information from a giant pool of data can help us be more efficient. For example, extracting events from business news aids users to perceive market trends, stay up to date with competitors' strategies and to make valuable investment decisioins.
