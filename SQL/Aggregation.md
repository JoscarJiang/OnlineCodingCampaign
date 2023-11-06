## sum
``` sql
SELECT SUM(population) FROM city WHERE district = "California"
```

## average
(The Blunder)[https://www.hackerrank.com/challenges/the-blunder/problem?isFullScreen=true]
```sql
SELECT CEIL(AVG(salary) - AVG(CAST(REPLACE(CAST(salary AS CHAR), "0", "") AS SIGNED))) FROM employees
```
### Note
- CEIL/CEILING: round it up to the next integer -> up. 
	- The opposite is FLOOR(): round it to smaller than or equal to the number
	- ROUND(number, decimals): rounds a number to a specified number of decimal places. decimals is optional:if empty, it returns integer.
	- TRUNCATE(number, decimals): truncates a number to the specified number of decimal places
	- CEIL(4.3) = 5, FLOOR(4.3) = 4, CEIL(-6.6) = -6, FLOOR(-6.6) = -7, ROUND(-6.6) = -7, TRANCATE(-6.6, 0) = -6
- CAST(value AS type): type can be DATE/DATETIME/DECIMAL/TIME/CHAR/SIGNED/UNSIGNED...
	- Attention: INT is not valid, use SIGNED 
	- The same as CONVERT(value, type). But convert can be also used to change charset as *CONVERT(value USING charset)*
- REPLACE: REPLACE(string, old_string, new_string)