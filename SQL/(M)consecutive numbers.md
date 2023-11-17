# Consecutive Numbers

Leetcode Link: https://leetcode.com/problems/consecutive-numbers/solutions/4261387/consecutive-numbers-mysql/


```sql
# Write your MySQL query statement below

with cte as (
    select num
    ,lead(num,1) over() num1
    ,lead(num,2) over() num2
    from logs
)
select 
    distinct num ConsecutiveNums 
from cte 
where (num=num1) and (num1=num2)


# SELECT DISTINCT num as ConsecutiveNums
# FROM logs
# WHERE (id + 1, num) IN (SELECT * FROM logs) AND (id + 2, num) IN (SELECT * FROM logs)

```

Learn Lead
https://docs.oracle.com/en/database/oracle/oracle-database/19/sqlrf/LEAD.html#GUID-0A0481F1-E98F-4535-A739-FCCA8D1B5B77
