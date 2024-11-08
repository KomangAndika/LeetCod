Table: Seat

+-------------+---------+
| Column Name | Type    |
+-------------+---------+
| id          | int     |
| student     | varchar |
+-------------+---------+
id is the primary key (unique value) column for this table.
Each row of this table indicates the name and the ID of a student.
The ID sequence always starts from 1 and increments continuously.
 

Write a solution to swap the seat id of every two consecutive students. If the number of students is odd, the id of the last student is not swapped.

Return the result table ordered by id in ascending order.

The result format is in the following example.

 

Example 1:

Input: 
Seat table:
+----+---------+
| id | student |
+----+---------+
| 1  | Abbot   |
| 2  | Doris   |
| 3  | Emerson |
| 4  | Green   |
| 5  | Jeames  |
+----+---------+
Output: 
+----+---------+
| id | student |
+----+---------+
| 1  | Doris   |
| 2  | Abbot   |
| 3  | Green   |
| 4  | Emerson |
| 5  | Jeames  |
+----+---------+
Explanation: 
Note that if the number of students is odd, there is no need to change the last one's seat.

## Solution
```{sql}
SELECT(
    CASE
    WHEN id%2 != 0 AND id != counts THEN id+1
    WHEN id%2 != 0 AND id = counts THEN id
    ELSE id-1
    END
) AS id, student
FROM seat, (SELECT count(*) as counts FROM seat)
AS seat_counts
ORDER BY id ASC
```

Basically we're playing with the id of the database,:
1. When the id is odd and not the last id, change it into the id after.
2. When the id is odd and the last id, nothing happend.
3. Else, or when it is even and not the last id, change into the id before.
After that the order may looked like from:
1 
2
3
4
5
Into:
2
1
4
3
5
Mind that we've only changed the id and it is still not in order, so we apply ORDER BY id and put ASC as it means ascending. :)