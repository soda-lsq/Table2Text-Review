# Table2Text Paper-Review


This is a review for the Logical table2text task, following the work of [wenhuchen](https://github.com/wenhuchen) from UCSB. Logical table2text task aims to generate a logical sentence from structured data of tables, involving both symbolic and linguistic inference. 

##  Relevent Paper List

| |conference|paper|code|
|----|-----|----|----|
|1|ICLR 2020|TabFact: A Large-scale Dataset for Table-based Fact Verification|https://github.com/wenhuchen/Table-Fact-Checking|
|2|ACL 2020|Logical Natural Language Generation from Open-Domain Tables|https://github.com/wenhuchen/LogicNLG|
|3|EMNLP 2020|KGPT: Knowledge-Grounded Pre-Training for Data-to-Text Generation|https://github.com/wenhuchen/KGPT|

## TabFact

### 1. Contribution

* Study the **fact verification** given **semi-structured table**.
  * *fact verification*: verify whether a textual hypothesis holds based on the given evidence. 
  * *semi-structured table*: unstructured evidence - natural language, document, structured evidence - tables, graphs, and databases. 

* Construct a large scale dataset **TabFact** (https://tabfact.github.io/) of 16k Wikipedia tables and 118k human-annoted natural language statements. **TabFact is the first dataset to evalaute language inference on strctured data.**

* Propose 2 different models: 
  * *Table-BERT*: regard the task as a NLI problem, use BERT to encode linearized tables and statements into continuous vectors. 
  * *Latent Program Algorithm (LPA)*: parse statements into progrmas and executes them against tables to obtain a binary value for verification.

### 2. Introduction

* Challenge: verification problem for structured data. As for sequence, we could use metrics like BLEU score or other scores, but it is hard to design a reasonable metric for logical inference from a table except human judgement. 

* Previous methods attempts to solve verification problem: logic rules, knowledge bases, and neural networks.

* Constructed a large-scale dataset called TabFact, and proposed 2 methods Table-Bert and LPA. 


### 3. Table Fact Verification Dataset (TabFact)

Tabfact is constructed based on WikiTables, with annotations from Amazon Mechanical Turk workers. Following a pipeline of "positive two channel annotation" -> "negative statement rewrinting" -> "verification" to ensure the annotation quality. 

#### 3.1 Positive Two-Channel Collection & Negative Rewriting Strategy
* Low-Reward Simple Channel: write 5 sentences to a single row/record in the table, (1) with unary fact without envolving logical inference, (2) mention the cell values without modification.
* High-Reward Complex Channel: write 5 sentences involving multiple rows in the table, (1) with higher-order semantics, like argmax, argmin, count, difference, average, summarize, etc. (2) repharse the table to involve more semantic understanding. This channel is harder for both linguistic and symbolic reasoning. 
* Negative samples: rewrite the collected entailed statements to revert the statement polarity, minimizing the obvious linguistic cues or patterns, turning **ENTAILED** statements into **REFUTED** ones.  

#### 3.2 Dataset Statics

The common higher-order operations are grouped into 8 categories, aggregation, negate, superlative, count, compative,  ordinal, unique, all (sample 200 sentences to visualize distribution). 

![](https://github.com/soda-lsq/Table2Text-Review/blob/main/dataset-statics.png?raw=true)

### 4. Models

**INPUTS:** a dataset of triple instances (T, S, L) - (Table, Statement, Label). Label = 0 or 1, ENTAILED L=1, REFUTED L=0.

**OUTPUTS:** label L of 0 or 1, a binary classification problem to predict labels. 

**METRIC:** prediction accuracy, the percentage of correct predictions on the test set. 

**ENTITY LINKING:** detect all the entities in the statements before building the model to find the exact cell words in the statement. First, lemmatize the statement, then find the longest substring that matches table cell words or captions. The matched phrases are denoted as the linked entities. 

#### 4.1 Latent Program Algorithm (LPA)

A weakly-supervised training algorithm designs a rule to search for latent candidate programs via pushing and popping the caches.  

#### 4.2 Table-BERT

Architecture of Table-BERT is **a BERT Encoder** + **a MLP Classifier**. 
1. How to encode a table? 
First, we need to specify a table's features and how to read a table to get its meaning. The table is structured data with header strings and cells. The meaning of a cell is reflected by the corresponding header string within the same column. The meaning of a row is a combination of certain cells, involving the meanings of several columns. 
Second, we need to think about how to encode the table with the above features. One way to encode structured data is to combine both sequence information as well as structural information. It is straightforward to get the sequence information since it could be fetched through cell contents. Table structure information can be viewed as a row number or column header string. As a result, the author proposed two different table linearization methods: **concatenation** and **template**.  

![](https://github.com/soda-lsq/Table2Text-Review/blob/main/Table-BERT.png?raw=true)

2. A MLP binary classifier, classify the (table, statememt) pair as ENTAILED statement when the probability is greater than 0.5.

## Logical NLG

