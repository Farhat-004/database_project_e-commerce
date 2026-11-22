# E-Commerce Database Project

An Oracle Database 21c Express Edition project that models the core data for a small e-commerce platform. The project includes database-user setup, table definitions, relationships, constraints, and sample records for users, products, orders, and order items.

## Technologies

- Oracle Database 21c Express Edition
- SQL*Plus
- Oracle SQL and PL/SQL-compatible DDL/DML scripts

## Project Files

| File | Description |
| --- | --- |
| `proj-ddl.txt` | Creates the `FARHAT` database user, grants privileges, creates the tables, and adds the required foreign key. |
| `proj-dml.txt` | Inserts sample users, products, orders, and order items, displays the records, and commits the transaction. |

## Database Schema

### `USERS`

Stores customer information:

- `USER_ID` - Primary key
- `USER_NAME`
- `ADDRESS`
- `PHONE`
- `POSTAL_CODE`
- `COUNTRY`
- `CITY`

### `PRODUCT`

Stores products available for purchase:

- `PRODUCT_ID` - Primary key
- `PRODUCT_NAME`
- `PRODUCT_PRICE`
- `PRODUCT_QUANTITY`

### `ORDERS`

Stores customer orders:

- `ORDER_ID` - Primary key
- `USER_ID` - Foreign key referencing `USERS(USER_ID)`
- `ORDER_DATE`
- `DELIVERY_DATE` - Required and must be later than `ORDER_DATE`
- `STATUS` - Must be `PENDING`, `SHIPPING`, or `DELIVERED`

### `ORDER_ITEMS`

Stores the products and quantities included in each order:

- `ORDER_ITEM_ID` - Primary key
- `ORDER_ID` - Foreign key referencing `ORDERS(ORDER_ID)`
- `PRODUCT_ID` - Foreign key referencing `PRODUCT(PRODUCT_ID)`
- `QUANTITY`
- `TOTAL_PRICE` - Required

## Relationships

- One user can place multiple orders.
- One order can contain multiple order items.
- Each order item references one product.
- Products are connected to orders through `ORDER_ITEMS`.

## Sample Data

The DML script includes:

- 10 customers from cities in Bangladesh
- 10 products, including laptops, smartphones, monitors, and accessories
- 10 orders with dates in November 2026
- Order statuses covering `PENDING`, `SHIPPING`, and `DELIVERED`
- 10 order-item records with quantities and calculated total prices

## Setup and Execution

1. Start an Oracle Database 21c XE instance and open SQL*Plus.
2. Review `proj-ddl.txt` and replace the example database credentials with secure credentials appropriate for your environment.
3. Run the DDL script as a user with permission to create users and grant privileges:

   ```sql
   @proj-ddl.txt
   ```

4. Connect as the project schema user and run the sample data script:

   ```sql
   @proj-dml.txt
   ```

5. Verify the inserted data with queries such as:

   ```sql
   SELECT * FROM USERS;
   SELECT * FROM PRODUCT;
   SELECT * FROM ORDERS;
   SELECT * FROM ORDER_ITEMS;
   ```

> Do not use the example password from the script in a production environment. Store credentials securely and avoid committing real credentials to source control.

## Constraints and Validation

- Primary keys uniquely identify users, products, orders, and order items.
- Foreign keys maintain relationships between users, orders, products, and order items.
- `DELIVERY_DATE` cannot be earlier than or equal to `ORDER_DATE`.
- Order status values are restricted to the three supported states.
- `DELIVERY_DATE` and `ORDER_ITEMS.TOTAL_PRICE` are required fields.

## License

No license has been specified for this project.
