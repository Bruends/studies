# SELECT
examples are tested in MySQL

## Basic SELECT
select all data from the table

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


## WHERE and ORDER BY 
WHERE: filter data that fulfill a condition  
ORDER BY: sort the results by column `ASC`(ascending) or `DESC`(descending)

example: 
```sql
    SELECT id, product, price, stock, category
    FROM tech_product
    -- only products more expensive than $1000
    WHERE price > 1000
    -- order the results (expensive to cheaper) 
    ORDER BY price DESC;
```

result: 
| id  | product  | price   | stock | category    |
|:---:|:--------:|:-------:|:-----:|:-----------:|
| 5   | Iphone   | 1566.00 | 25    | smartphone  |
| 2   | Android  | 1100.96 | 26    | smartphone  |


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

## Keywords

### LIKE
find values that match a specified pattern  
the pattern can use `%` and `_` wildcards for unknown characters    
`%` is equivalent to `zero or more characters`  
`_` is equivalent to `one character`  

example:
```sql
    SELECT id, product, price, stock, category 
    FROM tech_product
    -- return a product that have one character after 'ndr'
    -- and can have 0 or many characters after 'ndr'
    WHERE product LIKE '_ndr%';
```

result: 
| id | product  | price   | stock | category    |
|:--:|:--------:|:-------:|:-----:|:-----------:|
| 2  | Android  | 1100.96 | 26    | smartphone  |

### DISTINCT 
return only different values

example:
```sql
    SELECT DISTINCT category
    FROM tech_product;
```

result:
|   category  |
|:-----------:|
|   hardware  |
|  smartphone |
| peripherals |


### BETWEEN
return results in between specified values 

example:
```sql 
    SELECT id, product, price, stock, category
    FROM tech_product
    WHERE price BETWEEN 100 AND 1000;
```

result: 
| id | product  | price   | stock | category    |
|:--:|:--------:|:-------:|:-----:|:-----------:|
| 1  | RAM 8GB  | 250.00  | 50    | hardware    |
| 3  | Headset  | 103.98  | 54    | peripherals |


### IN
return the results that match to any of the values in the specified list

example:
```sql
    SELECT id, product, price, stock, category  
    FROM tech_product
    -- only products IN hardware or peripherals categories
    WHERE category IN ('hardware', 'peripherals');
```

result:
| id | product  | price   | stock | category    |
|:--:|:--------:|:-------:|:-----:|:-----------:|
| 1  | RAM 8GB  | 250.00  | 50    | hardware    |
| 3  | Headset  | 103.98  | 54    | peripherals |
| 4  | Keyboard | 98.99   | 66    | peripherals |