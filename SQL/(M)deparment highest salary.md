# Deparment highest salary

Leetcode Link: https://leetcode.com/problems/department-highest-salary/

```sql
with r_t as(
    select 
    name
    , salary
    , departmentId
    # Cannot use ROW_NUMBER(), will only get the first max result
    # use rank instead, it assigns the same rank to rows with equal values.
    ,RANK() OVER (PARTITION BY departmentId ORDER BY salary DESC) as rk
    from employee) 
select 
    b.name as Department 
    ,a.name as Employee 
    , a.salary as Salary 
from r_t a
left join Department b on a.departmentId  = b.id
where rk=1
```
ROW_NUMBER()

RANK() 

MAX() 

OVER (PARTITION BY departmentId ORDER BY salary DESC)
