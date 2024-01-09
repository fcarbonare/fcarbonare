# Query between dates

## Semana passada
```
SELECT * FROM your_table
WHERE your_date_column BETWEEN CURDATE() - INTERVAL 1 WEEK AND CURDATE() - INTERVAL 1 DAY;
```
