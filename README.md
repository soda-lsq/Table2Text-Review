# Table2Text-Review


This is a review for the Logical table2text task, following the work of [wenhuchen](https://github.com/wenhuchen) from UCSB. Logical table2text task aims to generate a logical sentence from structured data of tables, involving both symbolic and linguistic inference. 

##  Relevent Paper List

| |conference|paper|code|
|----|-----|----|----|
|1|ICLR 2020|TabFact: A Large-scale Dataset for Table-based Fact Verification|https://github.com/wenhuchen/Table-Fact-Checking|
|2|ACL 2020|Logical Natural Language Generation from Open-Domain Tables|https://github.com/wenhuchen/LogicNLG|
|3|EMNLP 2020|KGPT: Knowledge-Grounded Pre-Training for Data-to-Text Generation|https://github.com/wenhuchen/KGPT|

## TabFact

### Contribution

* Study the **fact verification** given **semi-structured table**.
  * *fact verification*: verify whether a textual hypothesis holds based on the given evidence. 
  * *semi-structured table*: unstructured evidence - natural language, document, structured evidence - tables, graphs, and databases. 

* Construct a large scale dataset **TabFact** of 16k Wikipedia tables and 118k human-annoted natural language statements. **TabFact is the first dataset to evalaute language inference on strctured data.**

* Propose 2 different models: 
  * *Table-BERT*: regard the task as a NLI problem, use BERT to encode linearized tables and statements into continuous vectors. 
  * *Latent Program Algorithm (LPA)*: parse statements into progrmas and executes them against tables to obtain a binary value for verification.

### Introduction

* Challenge: verification problem for structured data. As for sequence, we could use metrics like BLEU score or other scores, but it is hard to design a reasonable metric for logical inference from a table except human judgement. 

* Previous methods attempts to solve verification problem: logic rules, knowledge bases, and neural networks.

* Constructed a large-scale dataset called TabFact, and proposed 2 methods Table-Bert and LPA. 


### Table Fact Verification Dataset (TabFact)

Tabfact is constructed based on WikiTables, with annotations from Amazon Mechanical Turk workers. Following a pipeline of "positive two channel annotation" -> "negative statement rewrinting" -> "verification" to ensure the annotation quality. 

* Positive Two-Channel Collection & Negative Rewriting Strategy
 * Low-Reward Simple Channel: write 5 sentences to a single row/record in the table, (1) with unary fact without envolving logical inference, (2) mention the cell values without modification.
 * High-Reward Complex Channel: write 5 sentences involving multiple rows in the table, (1) with higher-order semantics, like argmax, argmin, count, difference, average, summarize, etc. (2) repharse the table to involve more semantic understanding. This channel is harder for both linguistic and symbolic reasoning. 
 * Negative samples: rewrite the collected entailed statements to revert the statement polarity, minimizing the obvious linguistic cues or patterns. 

* Dataset Statics


## Logical NLG

