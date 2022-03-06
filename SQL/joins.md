# joins
join table data

tables and data for the examples: 

product:
| id (PK)| product_name  | price   | stock | category_id (FK) |
|:------:|:-------------:|:-------:|:-----:|:----------------:|
| 1      | RAM 8GB       | 250.00  | 50    | 1                |
| 2      | Android       | 1100.96 | 26    | 3                |
| 3      | Headset       | 103.98  | 54    | 2                |
| 4      | Keyboard      | 98.99   | 66    | 2                |
| 5      | Iphone        | 1566.00 | 25    | 3                |

category:
| id (PK) | category_name |
|:-------:|:-------------:|
|  1      |    hardware   |
|  2      |  peripherals  |
|  3      |   smartphone  |
|  4      |     games     |
|  5      |       PC      |

`cardinality: product (1-n) --- (1) category`


## INNER JOIN
show `all matching` data in specified tables

example: 
```sql
    SELECT p.product_name, c.category_name 
    FROM product AS p
    -- only show products that have categories
    -- and categories that have products
    INNER JOIN category AS c ON c.id = p.category_id;
```

result:
| product_name | category_name |
|--------------|---------------|
| RAM 8GB      | hardware      |
| Android      | smartphone    |
| Headset      | peripherals   |
| Keyboard     | peripherals   |
| Iphone       | smartphone    |


## FULL JOIN
show `all` data from both tables  
(obs: mysql doesn't support FULL JOIN)

example: 
```sql
    SELECT p.product_name, c.category_name 
    FROM product AS p
    -- only show products that have categories
    -- and categories that have products
    FULL JOIN category AS c ON c.id = p.category_id;
```

result:
| product_name | category_name |
|--------------|---------------|
| RAM 8GB      | hardware      |
| Android      | smartphone    |
| Headset      | peripherals   |
| Keyboard     | peripherals   |
| Iphone       | smartphone    |
| null         | games         |
| null         | PC            |


## RIGHT and LEFT JOIN
show `all data from one table` and `only the matching values on the other`  

LEFT: all from left and matching from right
RIGHT: all from right and matching from left


example: 
```sql
    SELECT p.product_name, c.category_name 
    FROM product AS p
    -- show all categories that have or not a product
    -- only show products that have categories
    RIGHT JOIN category AS c ON c.id = p.category_id;
    -- LEFT JOIN will show the oposite
```

result:
| product_name | category_name |
|--------------|---------------|
| RAM 8GB      | hardware      |
| Android      | smartphone    |
| Headset      | peripherals   |
| Keyboard     | peripherals   |
| Iphone       | smartphone    |
| null         | games         |
| null         | PC            |