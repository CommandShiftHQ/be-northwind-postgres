# Update Exercises

1. Write a statement to change the `email` of every employee to `'not available'`.

```sql
  UPDATE 
    employees 
  SET 
    email_address = 'not available';
```

1. Write a statement to change the `email` of every employee to `'classified'` and set everybody's `first_name` to `Dave`.


```sql
  UPDATE 
    employees 
  SET 
    email_address = 'classified',
    first_name = 'Dave';
```

1. Write a statement to change `email` to `'super top secret'` and `last_name` to `McSalesman` for employees who's `job_title` is `Sales Representative`.

```sql
	UPDATE 
    	employees 
  	SET 
    	email_address = 'super top secret',
    	last_name = 'McSalesman'
	WHERE 
		job_title = 'Sales Representative';
```

3. Write a statement to change the `webpage` of all the employees in Seattle to the Wikipedia page for Seattle. 

```sql
	UPDATE 
    	employees 
  	SET 
    	web_page = 'https://en.wikipedia.org/wiki/Seattle'
	WHERE 
		city = 'Seattle';
```

Now that we've wrecked the `employees` table, let's look at the `customers`:

1. Elizabeth Andersen recently married Roland Wacker. They have requested that you update the customer table to reflect the fact that Roland has taken Elizabeth's last name. 

```sql
  UPDATE 
    customers
	SET 
    last_name = 'Anderson'
	WHERE 
    customers.id = '10'; 
```

1. They also requested that you change the `ship_name` and `ship_address` on any orders that have not yet shipped to Roland. The ship name should reflect Roland's new `last_name`. The new address should match Elizabeth's. 

You will have to check the `order_details_status` table to see which code from the `orders` table corresponds to the order already being shipped. Extra points if you complete this exercise using a `JOIN` statement to link `order_details_status` and `orders`.


```sql
  UPDATE orders
          LEFT JOIN
      orders_status ON orders.status_id = orders_status.id
  SET 
      orders.ship_name = 'Roland Andersen',
      orders.ship_address = '123 8th Street',
      orders.ship_city = 'Portland',
      orders.ship_state_province = 'OR'
  WHERE
      customer_id = 10
          AND orders_status.status_name != 'Shipped';
```
