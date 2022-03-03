table and data used in examples:

| id | product  | price   | stock | category    |
|:--:|:--------:|:-------:|:-----:|:-----------:|
| 1  | RAM 8GB  | 250.00  | 50    | hardware    |
| 2  | Android  | 1100.96 | 26    | smartphone  |
| 3  | Headset  | 103.98  | 54    | peripherals |
| 4  | Keyboard | 98.99   | 66    | peripherals |
| 5  | Iphone   | 1566.00 | 25    | smartphone  |

# WHERE
filter data that fulfill a condition

```sql
    SELECT id, product, price, stock, category
    FROM tech_product
    -- only items more expensive than $1000
    WHERE price > 1000
```
result: 
| id | product  | price   | stock | category    |
|:--:|:--------:|:-------:|:-----:|:-----------:|
| 2  | Android  | 1100.96 | 26    | smartphone  |
| 5  | Iphone   | 1566.00 | 25    | smartphone  |


# Keywords

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
