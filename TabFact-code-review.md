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















