Original Link: https://github.com/wenhuchen/Table-Fact-Checking

# About Data

## Raw Data (collected_data folder)

The folder **"collected_data"** contains the **raw data collected directly from Mechnical Turker**, all the text are lower-cased, containing foreign characters in some tables. There are two files, the r1 file is collected in the first round (simple channel), which contains sentences involving less reasoning. The r2 file is collected in the second round (complex channel), which involves more complex multi-hop reasoning. 

The data format is as follows:

```
Table-id: {
[
Statement 1,
Statement 2,
...
],
[
Label 1,
Label 2,
...
],
Table Caption
}
```

An example : a table of 7 statements: Table id "xxx.csv" + [7 statements] + [7 labels] + Table caption. (1 for ENTAILED, 0 for REFUTED)

```
  "2-1123463-2.html.csv": [
    [
      "alex yoong started in grid position 22",
      "driver jacques villeneuve for bar - honda constructor was on grid 9",
      "driver pedro de la rosa had 29 laps",
      "the time / retired for the driver on grid 18 was brakes",
      "pedro de la rosa was the driver with the second smallest number of laps",
      "enrique bernoldi was the driver on grid 9",
      "22 was the grid of driver eddie irvine"
    ],
    [
      1,
      1,
      1,
      1,
      0,
      0,
      0
    ],
    "2002 canadian grand prix"
```

## Data Organization (in a certain format)

Data are all in JSON format since reading quicker than txt.

* all_csv folder: it contains all the table files in the csv format.

* all_csv_ids.json: it contains all the table ids, all_csv_ids = complex_ids + simple_ids.

* train_ids.json, val_ids.json, test_ids.json: these contain the table ids used for training/validation/testing

* table_to_page.json links each table to its belonging wikipeia URL: Table ID "xxx.csv" + Table caption + URL

```
  "2-18847467-2.html.csv": [
    "1982 new orleans saints season", 
    "https://en.wikipedia.org/wiki/1982_New_Orleans_Saints_season"
  ]
```

# Data Preprocess
Input data: collected_data文件夹中收集的不同难度r1,r2的原始数据，数据格式为：table_id:[[statements], [labels], caption]
Output data: 生成tokenized_data文件夹中的full_cleaned.json，数据格式为：
# 数据预处理的流程：
* 数据处理采用多进程并行处理，会导致输出不是按照代码print的位置输出，因此在测试代码功能时采用单线程处理，即设置了pool=Pool(1)。
* 1. 读取原始数据的table_id，在all_csv中读取对应的table(table中各个cell的数值通过'#'分隔)，k是行号，_是每行对应的内容(k=0时对应表头内容)。依次从上至下的处理表格的每行，以及从左向右的处理每行的数据，两个#XX#中包含的是单元格内容。对于每个单元格内容，使用空格划分token，nltk.pos_tag()标注token的词性，同时使用tokenizer还原单词存入lemmatized_w中，对应的还原关系存入recover_dict中。
![](https://github.com/soda-lsq/Table2Text-Review/blob/main/Figures/data_preprocess.png)

* 2. 将token（lemmatized_w中的内容）对应在table中的位置（行列号）存入backbone，即{'token': [k, l]}，此时一个token可能对应多个行列号。
![](https://github.com/soda-lsq/Table2Text-Review/blob/main/Figures/Table-backbone.png)

* 以上是根据raw data中的table_id关联到Wikipedia表格得到的内容（主要是words[], pos_tags[], lemmatized_w[],以及整个表格对应的token与在表格中位置的映射backbone{}）。
接下来处理raw data中的其他数据，statements(entry[0]), lables(entry[1]), caption(entry[2])


![](https://github.com/soda-lsq/Table2Text-Review/blob/main/Figures/raw_data.png)

![](https://github.com/soda-lsq/Table2Text-Review/blob/main/Figures/csv_data.png)

![](https://github.com/soda-lsq/Table2Text-Review/blob/main/Figures/cleaned_data.png)






