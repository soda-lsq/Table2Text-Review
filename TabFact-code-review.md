Original Link: https://github.com/wenhuchen/Table-Fact-Checking

# About Data

## Raw Data

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

An example : a table of 7 statements: Table id "xxx.csv" + [7 statements] + [7 labels] + Table caption. 

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

