# User defined functions
## kruskal wallis 
Computes the test statistics (H) and the p value of the Kruskal Wallis test(https://en.wikipedia.org/wiki/Kruskal-Wallis_one-way_analysis_of_variance).

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
