# SELECT
return data from the table

example: 

```sql
    SELECT id, product, price, stock, category 
    FROM tech_product;

    -- OR 
    -- use the * symbol to get all the columns 
    SELECT * FROM tech_product;
```
result: 
| id | product  | price   | stock | category    |
|:--:|:--------:|:-------:|:-----:|:-----------:|
| 1  | RAM 8GB  | 250.00  | 50    | hardware    |
| 2  | Android  | 1100.96 | 26    | smartphone  |
| 3  | Headset  | 103.98  | 54    | peripherals |
| 4  | Keyboard | 98.99   | 66    | peripherals |
| 5  | Iphone   | 1566.00 | 25    | smartphone  |


## AS (alias)
to add an alias to the column name use the command `AS` 

example: 
```sql
    SELECT id, product, price, stock AS 'quantity'
    FROM tech_product;
```

result: 
| id | product  | price   | quantity |
|:--:|:--------:|:-------:|:--------:|
| 1  | RAM 8GB  | 250.00  | 50       |
| 2  | Android  | 1100.96 | 26       |
| 3  | Headset  | 103.98  | 54       |
| 4  | Keyboard | 98.99   | 66       |
| 5  | Iphone   | 1566.00 | 25       |


## ORDER BY 
sort the results by column `ASC`(ascending) or `DESC`(descending)

example: 
```sql
    SELECT id, product, price, stock, category
    FROM tech_product
    -- order the results (expensive to cheaper) 
    ORDER BY id DESC;
```

result: 
| id | product  | price   | stock | category    |
|:--:|:--------:|:-------:|:-----:|:-----------:|
| 5  | Iphone   | 1566.00 | 25    | smartphone  |
| 4  | Keyboard | 98.99   | 66    | peripherals |
| 3  | Headset  | 103.98  | 54    | peripherals |
| 2  | Android  | 1100.96 | 26    | smartphone  |
| 1  | RAM 8GB  | 250.00  | 50    | hardware    |


## GROUP BY and HAVING
GROUP BY: group rows that have the same value  
HAVING: filter data that fulfill a condition (in groups)

example: 
```sql
    -- show the amount of products in each category
    SELECT category, COUNT(product) as 'total_items' 
    FROM tech_product 
    -- group the duplicated categories
    GROUP BY category
    -- only categories that have at least 1 item
    HAVING COUNT(product) > 0;
```

result: 
|   category  | total_items |
|:-----------:|:-----------:|
|   hardware  |      1      |
|  smartphone |      2      |
| peripherals |      2      |


# Subquerys
a query inside another query, commonly used in WHERE conditions

example: 
```sql
    SELECT id, product, price
    FROM tech_product
    WHERE price = (
        -- find the most expensive item
        SELECT MAX(price)
        FROM tech_product
    );
```

result:
| id | product  | Price   | stock | category    |
|----|----------|---------|-------|-------------|
| 5  | Iphone   | 1566.00 | 25    | smartphone  |