# 197. Rising Temp
Table: Weather

+---------------+---------+
| Column Name   | Type    |
+---------------+---------+
| id            | int     |
| recordDate    | date    |
| temperature   | int     |
+---------------+---------+
id is the column with unique values for this table.
There are no different rows with the same recordDate.
This table contains information about the temperature on a certain day.
 

Write a solution to find all dates' id with higher temperatures compared to its previous dates (yesterday).

Return the result table in any order.

The result format is in the following example.

 

Example 1:

Input: 
Weather table:
+----+------------+-------------+
| id | recordDate | temperature |
+----+------------+-------------+
| 1  | 2015-01-01 | 10          |
| 2  | 2015-01-02 | 25          |
| 3  | 2015-01-03 | 20          |
| 4  | 2015-01-04 | 30          |
+----+------------+-------------+
Output: 
+----+
| id |
+----+
| 2  |
| 4  |
+----+
Explanation: 
In 2015-01-02, the temperature was higher than the previous day (10 -> 25).
In 2015-01-04, the temperature was higher than the previous day (20 -> 30).

## Answer
```{sql}
SELECT
    current_order.id
FROM
    Weather AS current_order
JOIN
    Weather AS previous_order
ON
    DATEDIFF(current_order.RecordDate, previous_order.RecordDate) = 1
WHERE
    current_order.temperature > previous_order.temperature;
```

So it is basically join the first table with the second table but second table is only one day apart.

Lets say i have this table:
id	RecordDate	Temperature
1	2024-11-01	15
2	2024-11-02	18
3	2024-11-03	16
4	2024-11-04	20
5	2024-11-06	21

The DATEDIFF join result would be:
- current_order.id = 2 (RecordDate = 2024-11-02) and previous_order.id = 1 (RecordDate = 2024-11-01) are 1 day apart.

- current_order.id = 3 (RecordDate = 2024-11-03) and previous_order.id = 2 (RecordDate = 2024-11-02) are 1 day apart.

- current_order.id = 4 (RecordDate = 2024-11-04) and previous_order.id = 3 (RecordDate = 2024-11-03) are 1 day apart.

- current_order.id = 5 (RecordDate = 2024-11-06) does not match any row since it has no row exactly one day before it.

and after that you just choose the current_order.id with the condition where the current temp is higher than yesterday.