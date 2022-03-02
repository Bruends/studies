# SELECT

## SELECT ALL
return all table data

example: 

```sql
    SELECT * FROM product;
```
result: 

| id | product  | Price   | stock | category    |
|:--:|:--------:|:-------:|:-----:|:-----------:|
| 1  | RAM 8GB  | 250.00  | 50    | hardware    |
| 2  | Android  | 1100.96 | 26    | smartphone  |
| 3  | Headset  | 103.98  | 54    | peripherals |
| 4  | Keyboard | 98.99   | 66    | peripherals |
| 5  | Iphone   | 1566.00 | 25    | smartphone  |


## SELECT columns 
return data from the specified columns
to add an alias to the column name use the command: `AS` 

example: 

```sql
    SELECT id, product, price, stock AS 'quantity'
    FROM product;
```

result: 

| id | product  | Price   | quantity |
|:--:|:--------:|:-------:|:--------:|
| 1  | RAM 8GB  | 250.00  | 50       |
| 2  | Android  | 1100.96 | 26       |
| 3  | Headset  | 103.98  | 54       |
| 4  | Keyboard | 98.99   | 66       |
| 5  | Iphone   | 1566.00 | 25       |


## WHERE and ORDER BY 
- WHERE: filter data that fulfill a condition
- ORDER BY: sort the results by column `ASC`(ascending) or `DESC`(descending)

example: 

```sql
    SELECT id, product, price, stock
    FROM product
    -- only products more expensive than $1000
    WHERE price > 1000
    -- order the results (expensive to cheaper) 
    ORDER BY price DESC;
```

result: 

| id  | product  | Price   | stock | category    |
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
    FROM product 
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