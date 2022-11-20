# Delete Exercises

1. Write a statement to delete the order with `id` = `30` from the orders table. This is trickier than it seems. Remember that foreign key constraints prevent us from deleting records that are referenced in other tables. To get around foreign key constraints, you can: manually delete related records from other tables, alter the table to enable [cascading deletes](https://www.postgresqltutorial.com/postgresql-tutorial/postgresql-foreign-key/) or remove foreign key constraints (temporarily or permanently). Think about the advantages and disadvantages of each of these options. 
2. Delete any orders that are shipping to `New York`.
3. Delete any discontinued products from the `product` table.
4. Pick a customer, delete them, any orders they have made, and any related data in the `order_details` table. Consider foreign key constraints again!
5. Delete the entire `employee` table. You might want to check the [`TRUNCATE`](https://www.postgresql.org/docs/current/sql-truncate.html) command.
