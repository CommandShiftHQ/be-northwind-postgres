# Delete Exercises

Now that we've got to grips with creating, reading and updating data in our database, it's time to watch the world burn 🔥.

1. Write a statement to delete the order with `id` = `30` from the orders table. This is trickier than it seems. Remember that foreign key constraints prevent us from deleting records that are referenced in other tables. To get around foreign key constraints, you can: manually delete related records from other tables, alter the table to enable [cascading deletes](https://www.postgresqltutorial.com/postgresql-tutorial/postgresql-foreign-key/) or remove foreign key constraints (temporarily or permanently). Think about the advantages and disadvantages of each of these options. 

```sql
-- There are two Foreign Keys that need updating. 
-- We first need to drop them then re-create the constraints with option to propagate deletions.
	
-- First dropping the invoices FK
  ALTER TABLE invoices
  DROP CONSTRAINT fk_invoices_orders1;

-- Then recreate it with ON DELETE CASCADE option
  ALTER TABLE invoices
  ADD CONSTRAINT fk_invoices_orders1 FOREIGN KEY (order_id)
  REFERENCES public.orders (id) MATCH SIMPLE
    ON UPDATE CASCADE
    ON DELETE CASCADE;

-- Secondly the order_details FK
  ALTER TABLE order_details
  DROP CONSTRAINT fk_order_details_orders1;

-- Then recreate it with ON DELETE CASCADE option
  ALTER TABLE order_details
  ADD CONSTRAINT fk_order_details_orders1 FOREIGN KEY (order_id)
    REFERENCES public.orders (id) MATCH SIMPLE
    ON UPDATE CASCADE
    ON DELETE CASCADE;

-- Finally the order can be dropped and changes will be cascaded
  DELETE FROM orders
  WHERE orders.id = 30;
```

2. Delete any orders that are shipping to `New York`.

```sql
	DELETE FROM orders
	WHERE orders.ship_city = 'New York';
```

3. Delete any discontinued products from the `product` table.

```sql
    ALTER TABLE inventory_transactions
    DROP CONSTRAINT fk_inventory_transactions_products1;

    ALTER TABLE inventory_transactions
    ADD CONSTRAINT fk_inventory_transactions_products1 FOREIGN KEY (product_id)
          REFERENCES public.products (id) MATCH SIMPLE
          ON UPDATE CASCADE
          ON DELETE CASCADE;

    ALTER TABLE order_details
      DROP CONSTRAINT fk_order_details_products1;

    ALTER TABLE order_details
    ADD CONSTRAINT fk_order_details_products1 FOREIGN KEY (product_id)
          REFERENCES public.products (id) MATCH SIMPLE
          ON UPDATE CASCADE
          ON DELETE CASCADE;

    ALTER TABLE purchase_order_details
      DROP CONSTRAINT fk_purchase_order_details_products1;

    ALTER TABLE purchase_order_details
    ADD CONSTRAINT fk_purchase_order_details_products1 FOREIGN KEY (product_id)
          REFERENCES public.products (id) MATCH SIMPLE
          ON UPDATE CASCADE
          ON DELETE CASCADE;


    DELETE FROM products 
    WHERE discontinued = 1;
```

4. Pick a customer, delete them, any orders they have made, and any related data in the `order_details` table. Consider foreign key constraints again!

```sql
	ALTER TABLE orders
  DROP CONSTRAINT fk_orders_customers;
	
	ALTER TABLE orders
	ADD CONSTRAINT fk_orders_customers FOREIGN KEY (customer_id)
    REFERENCES public.customers (id) MATCH SIMPLE
    ON UPDATE CASCADE
    ON DELETE CASCADE;
	
	DELETE FROM customers WHERE customers.id = 1;
```

5. Delete the entire `employee` table. You might want to check the [TRUNCATE](https://www.postgresql.org/docs/current/sql-truncate.html) command.
```sql
  TRUNCATE TABLE employees CASCADE;
```

For this exercise, you can also use the `DROP TABLE employees` solution, but like in previous exercises, you will need to update all the Foreign Key Constraints.
