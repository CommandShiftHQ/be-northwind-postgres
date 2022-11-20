# Read Exercises

These exercises all require you to read data from the `products` table.

1. Write a query to get Product `name` and `quantity per unit`.

```sql
  SELECT 
    product_name, quantity_per_unit
  FROM
    products;
```

1. Write a query to get a list of currently available products (`id` and `name`).

```sql
  SELECT 
    product_name, quantity_per_unit
  FROM
    products
  WHERE
    discontinued = 0;
```

1. Write a query to get a list of discontinued products (`id` and `name`).

```sql
  SELECT 
    product_name, quantity_per_unit
  FROM
    products
  WHERE
    discontinued = 1;
```

1. Write a query to get the name and price of the most expensive product.

```sql
  SELECT 
    product_name, list_price
  FROM
      products
  WHERE
    list_price = (SELECT MAX(list_price) from products);
  ```

1. Write a query to get the name and price of the least expensive product.

```sql
  SELECT 
    product_name, list_price
  FROM
    products
  WHERE
    list_price = (SELECT MIN(list_price) from products);
```


1. Write a query to get a list of products that cost less than $20.

```sql
  SELECT 
    product_name, list_price
  FROM
      products
  WHERE
    list_price < 20;
```

1. Write a query to get a list of products that cost between $15 and $25.

```sql
  SELECT 
    product_name,
      list_price
  FROM
      products
  WHERE
    list_price < 25 AND list_price > 15;
```

1. Write a query to get a list of the ten most expensive products.

```sql
  SELECT 
    product_name, list_price
  FROM
      products
  ORDER BY
    list_price DESC
  LIMIT 10;
```

1. Write a query to get the count of all the current products and then the count of all the discontinued products.

```sql
  SELECT 
    count(product_name)
  FROM 
    products
  GROUP BY 
    discontinued;
```
