# User defined functions
BigQuery now supports [User Defined Functions (UDFs)](https://cloud.google.com/bigquery/docs/reference/standard-sql/user-defined-functions) in SQL and JavaScript that can extend BigQuery on more specialized computations. To facilitate the analysis of cancer data, ISB-CGC offers a set of UDFs that implement commonly used statistical tests and methods in cancer research and bioinformatics, the source code of the ISB-CGC UDFs are hosted in this repo; and the following sections provide detailed descriptions and examples of how to use these functions in the [BigQuery console](https://console.cloud.google.com/bigquery).  

## kruskal_wallis 
Computes the test statistics (H) and the p value of the Kruskal Wallis test (https://en.wikipedia.org/wiki/Kruskal-Wallis_one-way_analysis_of_variance).

- **Input:** Data in form of an array of structures <factor STRING, val FLOAT64> where factors is the categorical or nominal data point and val is the numerical value (type array: struct <factor STRING, val FLOAT64>).
- **Output:** A structure of the type struct<H FLOAT64, p FLOAT64, DOF FLOAT64> where H is the statistic, p is the p value, and DOF is the degrees of freedom

#### Example
```
WITH mydata AS (
   SELECT [
    ('a',1.0), ('b',2.0), ('c',2.3), ('a',1.4),
    ('b',2.2), ('c',5.5), ('a',1.0), ('b',2.3),
    ('c',2.3), ('a',1.1), ('b',7.2), ('c',2.8)
   ] as data
) 
SELECT `isb-cgc-bq.functions.kruskal_wallis_current`(data) 
       AS results
FROM mydata
```

#### Output:
| results.H  | results.p  | results.DoF  |
|---|---|---|
| 3.423076923076927  | 0.1805877514841956  |  2 | 
