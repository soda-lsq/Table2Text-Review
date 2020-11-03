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
  * *Table-BERT*: use BERT to encode linearized tables and statements into continuous vectors. 
  * *Latent Program Algorithm (LPA)*: parse statements into progrmas and executes them against tables to obtain a binary value for verification.




## Logical NLG

