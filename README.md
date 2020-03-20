# Conceptual

Relational Databases are made of tables  
Tables are made of rows and columns  
Rows and columns are sometimes called records and fields, respectively 

## Definitions

**Column** - represents some sort of entity, like the amount of an invoice  
**Row** - contains a set of values for a single instance of the entity  
**Cell** - interection of the rows and columns   
**Primary key** - uniqueily identifies each row in the table. Usually a single column, but can be more than 1 column   
**Composite primary key** - when a primary key uses two or more columns  
**Unique key** - MySQL specific, not all dbs let you define one  
Non-primary key. Uniquely identifies each row in the table  
**Index** - provides an efficient way to access data from a table based on the values in specific columns  
Created automatically for a tables primary and non-primary keys  
**Foreign key** - one or more columns in a table that refer to a primary key in another table (one-to-many relationship)  
**Referential integrity** - makes sure that any changes to the data in the db do not create invalid relationships between tables.  
**Data type** - determines the type of information that is stored in the column  
Try to assign the data type that minimizes the use of disk storage because that improves the performance of queries later  
```
CHAR, VARCHAR 
INT, DECIMAL
FLOAT  
DATE
```
**Null** - value that is unknown, unavailable, or not applicable  
**Default value** - value that is assigned to the column if another value is not provided  
**Auto increment column** - value is generated automatically by the DBMS  
**Entity-relationship (ER)** or **enhanced entity-relationship (EER)** diagram - used to show how the tables in a database are defined and related  
**Result set/table** - the data that is returned by a query  
**DML** - data manipulation language - statements tha work with the data in a db 
  **SELECT** - gets data from one or more tables 
  **INSERT** - adds new rows to a table 
  **UPDATE** - changes existing rows in a table 
  **DELETE** - deletes existing rows from a table 
**DDL** - data definition language - statements that create databases and work with the objects within a db (usually used by db admins)
  **CREATE DATABASE** - creates a new db on the server 
  **CREATE TABLE** - creates a new table in a db 
  **CREATE INDEX** - creates a new index for a table 
  **ALTER TABLE** - changes the definition of an existing table 
  **ALTER INDEX** - changes the structure of an existing index 
  **DROP DATABASE** - deletes an existing db and all of its tables 
  **DROP TABLE** - deletes an existing table 
  **DROP INDEX** - deletes an existing index 

**Database object** - any defined object in a db that is used to store or reference data. 
Anything that is created from a CREATE command is a db object, including: 
- Table 
- View
- Sequence
- Index 
- Synonym

## Building queries 
    Best practice to build queries one clause at a time.

# Statements 
**SELECT** - clause that names the columns to be retrieved
**INSERT INTO** - clause that names the columns whose values are supplied in the **VALUES** clause 
**VALUES** - clause that lists the data that is inserted with an **INSERT** clause
**UPDATE** - clause that changes the data in one or more rows of a table
**DELETE** - clause that deletes one or more rows from a table 
**FROM** - clause that names the base table from which the query retrieves the data 
**AS** - clause that assigns a new name to a group of columns. The new name is the column alias 
Called a calculated value because it exists only in this query 
When there is a space in the alias name, enclose the alias name in quotes. For example, 'Test Row'
**WHERE** - clause that filters the rows in the base table by the boolean expression that takes a true, false, or NULL value. For example, **WHERE** value > 0
If you omit the **WHERE** clause, all the rows in the base table are returned 

**IN** - used in **WHERE** clause. Compares the value of the test expression with the list of expressions in the IN phrase. If the test expression is equal to one of the expressions in the list, the row is included in the query results and each of the expressions in the list is converted to the same thpe of data as the test expression automatically. 
> Example:  
```sql
WHERE terms_id IN (1, 2, 3);
```
```sql
WHERE vendor_state NOT IN ('CA', 'NV', 'OR');
```
**BETWEEN** - used in **WHERE** clause. Compares the value of the test expression to the range of values specified in the BETWEEN phrase. If the value falls within this range, it is included in the results. You can use the NOT operator with this.
> Example:
```sql
WHERE invoice BETWEEN '2018-06-01' AND '2018-06-30';
```
```sql
WHERE  vendor_zip_code NOT BETWEEN 93600 AND 93799;
```
**LIKE** or **REGEXP** - used in the **WHERE** clause. Use to retrieve rows that match a specific string pattern or mask. 
            **LIKE** Wildcards: 
                % - matches any string of zero or more characters 
                    **WHERE** vendor_city LIKE 'SAN%'; returns San Diego, Santa Ana
                _ - matches any single character 
                    **WHERE** vendor_name LIKE 'COMPU_ER'; returns Compuserve, Computerworld
            REGEXP special characters/constructs:
                ^ - matches the pattern to the beginning of the value being tested 
                    **WHERE** vendor_city REGEXP '^SA'; returns Pasadena, Santa Ana
                $ - matches the pattern to the end of the value being tested
                    **WHERE** vendor_city REGEXP 'NA$'; returns Gardena, Pasadena 
                . - matches any single character 
                [charlist] - mathces any single character listed within the brackets
                    **WHERE** vendor_city REGEXP 'N[CV]'; returns NC, NV but not NJ or NY 
                [char1 - char2] - matches any single character within the given range 
                    **WHERE** vendor_city REGEXP 'N[A-J]'; returns NC, NV but not NJ or NY 
                | - separates two string patterns and matches either one
                    **WHERE** vendor_city REGEXP 'RS|SN'; returns Trave(rs)e City, Fre(sn)o

                    **WHERE** vendor_city REGEXP '[A-Z][AEIOU]N$'; returns any vendor_city that ends with any letter, then a vowel, then the letter 'n'
        IS NULL - used in **WHERE** clause. Can use IS NOT NULL too.
            Example:
                **SELECT** * FROM null_sample 
                **WHERE** invoice_total = 0;

                **SELECT** * 
                FROM null_sample 
                **WHERE** invoice_total IS NOT NULL;


    ORDER BY - the clause that specifies the sort order for the rows in the result set. ASC is the default. 
        Can use column names, ASC, DESC, expressions, alias, column positions.
        To sort by more than one column, you list the values in the ORDER BY clause in the order that you want them sorted by. Called a nested sort. 
            Example:
                **SELECT** vendor_name,
                    CONCAT(vendor_city, ', ', vendor_state, ' ', vendor_zip_code) AS address 
                FROM vendors 
                ORDER BY vendor_name DESC;

                **SELECT** vendor_name,
                    CONCAT(vendor_city, ', ', vendor_state, ' ', vendor_zip_code) AS address
                FROM vendors
                ORDER BY CONCAT(vendor_contact_last_name, vendor_contact_first_name);

    LIMIT - the clause that specifices the maximum number of rows or the range of rows (using offset) that are returned in the result set. Usually after the ORDER BY clause. 
        LIMIT [offset, ] row count
        The offset is 0-indexed, so the following clause returns 5 rows that start at the index 3:
            Example: 
                **SELECT** invoice_id, vendor_id, invoice_total
                FROM invoices
                ORDER BY invoice_id
                LIMIT 2, 3;

    **SELECT** filters the columns, **WHERE** filters the rows 

        Model

        **SELECT** column_1, column_2, column_3 AS new_column_name
        FROM table_1
        WHERE column_1 - column_2 > 0
        ORDER BY column_1 
## SELECT 
    Syntax 
        SELECT select_list 
        [FROM table_source]
        [WHERE search_condition]
        [ORDER BY order_by_list]
        [LIMIT row_limit]
    Testing
        Use SELECT clauses without a FROM clause to test expressions and functions.
            Example:
                SELECT CURRENT_DATE,
                    DATE_FORMAT(CURRENT_DATE, '%m/%d/%y') AS 'MM/DD/YY',
                    DATE_FORMAT(CURRENT_DATE, '%e-%b-%Y') AS 'DD-Mon-YYYY';

                SELECT 12345.6789 AS value,
                    ROUND(12345.6789) AS nearest_dollar,
                    ROUND(12345.6789, 1) AS nearest_dime;
    DISTINCT - use DISTINCT if you do not want the results table to include duplicate rows. 


## Column specifications
    Base table value 
        All columns = *
        Column name = column_name 
    Calculated value 
        Result of a calculation = arithmetic expression
        Result of a function = functions (CONCAT, etc.)

## Arithmetic operators 
    *
    /
    DIV - integer division
    % (MOD)
    +
    -

## Logical operators 
    AND and OR - combine two or more search conditions in to a compound condition 
        Example: 
            WHERE vendor_state = 'NJ' AND vendor_city = 'Springfield';
            WHERE vendor_state = 'NJ' OR vendor_city = 'Springfield';
    NOT - used to negate a search condition 
        Example:
            WHERE NOT vendor_state = 'CA';
            Vendors in CA are not returned
    Order of precedence
        1. NOT
        2. AND
        3. OR

## Functions 
    Functions are used in the SELECT clause 
    CONCAT - used to join strings. 
        CONCAT(string1[, string2]...)
        Example:
            SELECT  vendor_name,
                    CONCAT(vendor_city, ', ', vendor_state, ' ', vendor_zip_code)
                        AS address 
            FROM vendors;
    LEFT - used to extract the x amount of characters from the left of the results of the query 
        Example: 
            LEFT(column_name, x)
            LEFT(vendor_contact_first_name, 1) 

            SELECT  vendor_contact_first_name, vendor_contact_last_name,
                CONCAT(LEFT(vendor_contact_first_name, 1),
                       LEFT(vendor_contact_last_name, 1)) AS initials
            FROM vendors;
    DATE_FORMAT - specify the format of a date. use the % signto identify a format code.
        For example, '%m/%d/%y' returns 04/08/18

    ROUND - rounds the value of the column to the nearest place, depending on the optional parameter.
        ROUND(nearest_penny, 2) returns 12.21
        ROUND(nearest_dime, 1) returns 12.2
    CURRENT_DATE - returns the current date 


## JOINS
    Retrives data from two tables and joins it together in a single result set 
        INNER JOIN - most common type of join. 
        Rows from the two tables in the join are included in the result table only if their related columns match.
            These columns are specified in the FROM clause of the SELECT statement. 

    Example: 
        SELECT vendor_name, invoice_number, invoice_date, invoice_total (1)
        FROM vendors INNER JOIN invoices (2)
            ON vendors.vendor_id = invoices.vendor_id (3)
        WHERE invoice_total >= 500 (4)
        ORDER BY vendor_name, invoice_total DESC; (5)

        (1) SELECTs 4 rows FROM the vendors table that it will use in the result set
        (2) Defines the two tables that it wants to use to create an INNER JOIN (vendors and invoices)
        (3) Defines the common column(s) that must exist in each table (vendor_id)
            If a vendor in the vendors tables does not have an invoice listed in the invoices table, then it is not in the results table for this INNER JOIN. For example, a new vendor that has not yet generated an invoice.
        (4) Filters the overlapping column by a value 
        (5) Sorts the column 
        
        
        , then includes the rows only if the value of the vendor_id column in the vendors table matches the value of the vendor_id column in one or more rows in the invoices table. 
        Then, it filters the results 
        If there are not any invoices for a particular vendor, that vendor is not included in the result set.

# Retrieve data from multiple tables 

## INNER JOIN
    Combines columns from 2 or more tables into a result set based on the join conditions
    For inner joins, only the two rows that satisfy the join condition are included in the result set 
    How to code inner join:
        Code the names of the 2 tables in the FROM clause along with the JOIN keyword and an ON phrase that specifies the join condition
        Example: 
            SELECT invoice_number, vendor_name              (1)
            FROM vendors INNER JOIN invoices                (2)
                ON vendors.vendor_id = invoices.vendor_id   (3)
            ORDER BY invoice_number;                        (4)

            (1) Standard SELECT clause 
            (2) FROM clause that names the two tables that are joined 
                'INNER' keyword is optional
            (3) ON phrase that names the columns where the tables are joined and how they are compared 
                columns preceded by 'table_name.' are called 'qualified columns' because you have explain which table they came from 
            (4) Standard ORDER BY clause 

    Implicit syntax 
        Not used often, prefer Explicit syntax outlined above. 
        Code the tables in the FROM clause separated by commas. 
        Example: 
            SELECT invoice_number, vendor_name
            FROM vendors v, invoices i  (1)
            WHERE v.vendor_id = i.vendor_id
            ORDER BY invoice_number;

            (1) Table names are separated by commas instead of 'INNER JOIN'

    Table aliases 
        An alternative table name thats typically just a letter or two. Like a variable.
        Makes the statement easier to read. 
            Example:
                SELECT  invoice_number, vendor_name, invoice_due_date,
				invoice_total - payment_total - credit_total AS balance_due
                FROM vendors v JOIN invoices i  (1)
                    ON v.vendor_id = i.vendor_id    (2)
                WHERE invoice_total - payment_total - credit_total > 0
                ORDER BY invoice_due_date DESC;

                (1) FROM clause that names the two tables and assigns them aliases 
                (2) use the aliases to qualify the columns 
    JOIN to a table in another db 
        Tables are organized into databases, which are also called schemas 
        Example: 
            SELECT vendor_name, customer_last_name, customer_first_name,
                vendor_state AS state, vendor_city AS city
            FROM vendors v
                JOIN om.customers c (1)
                ON v.vendor_zip_code = c.customer_zip
            ORDER BY state, city;

            (1) 'om' is the name of the db, 'customers' is the name of the table, 'c' is the name of the table alias 

    Compound JOIN 
        Create two or more comparisons in a join condition using the AND or OR operators 
        Example: 
            SELECT customer_first_name, customer_last_name
            FROM customers c JOIN employees e 
                ON c.customer_first_name = e.first_name
                AND c.customer_last_name = e.last_name; (1)
            (1) Return first and last names of all customers in the Customers table whose first and last names also exist in the Employees table. 
    Self JOIN 
        Joins a table to itself. Useful for retrieving data that can't be retrieved any other way. 
        Example: 
            SELECT DISTINCT v1.vendor_name, v1.vendor_city,
                v1.vendor_state
            FROM vendors v1 JOIN vendors v2     (1)
                ON v1.vendor_city = v2.vendor_city AND      (2)
                    v1.vendor_state = v2.vendor_state AND
                    v1.vendor_name = v2.vendor_name
            ORDER BY v1.vendor_state, v1.vendor_city;

            (1) Use aliases to distinguish one occurence of the table from the other 
            (2) Returns rows from the vendors table where the vendor is in a city and state that has at least one other vendor. 
                It does not return a vendor if that vendor is th only vendor in that city and state. 
    
    JOIN more than two tables
        Example:
            This example joins tables based on the relationship between the primary key of one table and a foreign key of the other table. 
            The account_number column is the primary key of the General_Ledger_Accounts table and a foreign key of the Invoice_Line_Items table 

            SELECT vendor_name, invoice_number, invoice_date,
                line_item_amount, account_description
            FROM vendors v
                JOIN invoices i
                    ON v.vendor_id = i.vendor_id
                JOIN invoice_line_items li
                    ON i.invoice_id = li.invoice_id
                JOIN general_ledger_accounts gl
                    ON li.account_number = gl.account_number
            WHERE invoice_total - payment_total - credit_total > 0
            ORDER BY vendor_name, line_item_amount DESC;

## OUTER JOINS 
    Returns all of the rows from one of the tables involved in the join, plus unmatched rows in the LEFT or RIGHT table, regardless of whether the join condition is true 
    LEFT or RIGHT keyword 
        LEFT - the result set includes all the rows from the first (left) table 
        RIGHT - the result set includes all the rows from the second (right) table 
        Example: 
        The following joins the vendors and invoices tables, and includes rows from the vendor column even if no matching invoices are found. If none are found, null vbalues are returned for those columns. 

        Example 1:
            SELECT vendor_name, invoice_number, invoice_total
            FROM vendors LEFT JOIN invoices
                ON vendors.vendor_id = invoices.vendor_id 
            ORDER BY vendor_name;

        Example 2:
        Combination of INNER and OUTER JOIN
            SELECT department_name, last_name, project_number
            FROM departments d  
                JOIN employees e
                    ON d.department_number = e.department_number
                LEFT JOIN projects p 
                    ON e.employee_id = p.employee_id
            ORDER BY department_name, last_name;

## USING keyword 
    Use the USING clause instead of an ON clause during an equijoin to specify the join. To join tables by multiple columns, put the multiple columns in the parentheses, separated by a column 
        equijoin/equi-join - When you use the equal operator to join two tables on a common column. 
            Common for the columns that are being compared to have the same name.
        
        Example 1:
            SELECT invoice_number, vendor_name
            FROM vendors
                JOIN invoices USING (vendor_id) (1)
            ORDER BY invoice_number;

            (1) USING (vendor_id) replaced 'ON vendors.vendor_id = invoices.vendor_id'
        
        Example 2:
            SELECT department_name, last_name, project_number
            FROM departments
                JOIN employees USING (department_number)    (1)
                LEFT JOIN projects USING (employee_id)      (2)
            ORDER BY department_name;

            (1) INNER JOIN between departments and employees on the department_number column 
            (2) LEFT JOIN between employees and projects using the employee_id column 

## NATURAL keyword 
    You don't specific the column that's used to join the two tables. The db joins the two tables based on all columns in the two tables that have the same name.

        Example: 
            SELECT department_name AS dept_name, last_name, project_number
            FROM departments
                NATURAL JOIN employees                      (1)
                LEFT JOIN projects USING (employee_id)      (2)
            ORDER BY department_name;

            (1) JOINs departments and employees on columns where they intersect
            (2) Creates a LEFT JOIN between employees and projects on employee_id column 

## CROSS JOINs 
    Produces a result set that includes each row from the first table joined with each row from the second table. 
    Result set is called a Cartesian product 

    Example:
        SELECT departments.department_number, department_name, employee_id, last_name
        FROM departments CROSS JOIN employees   (1)
        ORDER BY departments.department_number;

        (1) JOIN the 4 columns together in a result set from left to right, not based on where they intersect

## UNIONs 
Used to connect two or more SELECT statements. The result set of each SELECT statement must have the same number of columns, and the data types of the corresponding columns in each table must be compatible. 

Combines data from two or more result sets, instead of base tables.
To sort the result of a UNION, add an ORDER BY cluase after the last SELECT statement.
By default, UNIONs eliminates duplicate rows. To include dupes, add ALL keyword.
Column names in the final result set are taken from the first SELECT clause.

> Example: 
```sql
    SELECT invoice_number, vendor_name, '33% Payment' AS payment_type,
    invoice_total AS total, invoice_total * 0.333 AS payment
    FROM invoices JOIN vendors
        ON invoices.vendor_id = vendors.vendor_id
    WHERE invoice_total > 10000
UNION
    SELECT invoice_number, vendor_name, '50% Payment' AS payment_type,
        invoice_total AS total, invoice_total * 0.5 AS payment
    FROM invoices JOIN vendors
        ON invoices.vendor_id = vendors.vendor_id
    WHERE invoice_total BETWEEN 500 AND 10000
UNION
    SELECT invoice_number, vendor_name, 'Full amount' AS payment_type,
        invoice_total AS total, invoice_total AS payment
    FROM invoices JOIN vendors
        ON invoices.vendor_id = vendors.vendor_id
    WHERE invoice_total < 500
ORDER BY payment_type, vendor_name, invoice_number;
```
        
> Example:
> Combining result sets from the same table.
```sql
    SELECT 'Active' AS source, invoice_number, invoice_date, invoice_total  (1)
    FROM invoices 
    WHERE invoice_total - payment_total - credit_total > 0
UNION 
    SELECT 'Paid' AS source, invoice_number, invoice_date, invoice_total    (2)
    FROM invoices 
    WHERE invoice_total - payment_total - credit_total <= 0
ORDER BY invoice_total DESC;
```

(1) Rows that have a balance due. Adds column named 'source' to indicate that each row is 'Active'
(2) Rows that are paid in full. Adds column named 'source' to indicate that each row is 'Paid'
    
### Simulate a FULL OUTER JOIN with a UNION 
Simulate a FULL OUTER JOIN by creating a UNION that combines the result sets for a left outer join and a right outer join.
NULL is displayed in rows with no values 

> Example: 
```sql
    SELECT department_name AS dept_name, d.department_number AS d_dept_no,
        e.department_number AS e_dept_no, last_name
    FROM departments d
        LEFT JOIN employees e
        ON d.department_number = e.department_number
UNION
    SELECT department_name AS dept_name, d.department_number AS d_dept_no,
        e.department_number AS e_dept_no, last_name
        FROM departments d
            RIGHT JOIN employees e
            ON d.department_number = e.department_number
ORDER BY dept_name;
```

## Create

Create a copy of the table to do testing with the following statement:  

```sql
CREATE TABLE invoices_copy AS
SELECT *
FROM invoices;
```
Whey you create tables like this, MySQL copies only the column defnitions and data, not the primary keys, foreign keys, or indexes. 

## INSERT

Usually use this statement to add a single row to a table. Can also add multiple rows. You name the table on the INSERT clause, then add an optional list of columns, then add the new row

> **Example**
```sql
INSERT INTO invoices (1)
   (vendor_id, invoice_number, invoice_total, terms_id, invoice_date, invoice_due_date) (2)
VALUES (3)
   (97, '456789', 8344.50, 1, '2018-08-01', '2018-08-31');
```
1. **INSERT INTO** clause that names the base table
2. Optional list of columns  
   If you do not include a column list in the INSERT INTO clause, you must specify the values in the same order as in the table, and there must be a value for each column. To add multiple rows, specify multiple (value) lines in the INSERT clause.  
   Use **NULL** to insert a NULL.
   Use **DEFAULT** to insert the default value or if a value is defined as autoincrement.
3. **VALUES** clause that lists the values to add to the new row

   You can omit columns that have default valudes, accept null values, or are automatically generated.

### Subquery in INSERT statement

A **subquery** is a **SELECT** statement that is coded within another SQL statement. 
> **Example**  
> The subquery specifies the values for the new rows by selecting these values from another table. 

```sql
INSERT INTO invoice_archive
   (invoice_id, vendor_id, invoice_number, invoice_total, credit_total, payment_total, terms_id, invoice_date, invoice_due_date)
SELECT 
    invoice_id, vendor_id, invoice_number, invoice_total, credit_total, payment_total, terms_id, invoice_data, invoice_due_date
FROM invoices
WHERE invoice_total - payment_total - credit_total = 0;
```  

When you include a column list, you must list the columns in the same sequence as the **SELECT** clause of the subquery.  
You can omit auto increment columns, columns that are defined with default values, and columns that allow null values.

## UPDATE 
Use the **UPDATE** statement to modify the data in one or more rows in the table.

> **Example**
> Update two columns for a single row  
```sql
UPDATE invoices                     (1)
SET payment_date = '2018-09-21',    (2)
   payment_total = 19351.18    
WHERE invoice_number = '97/522';    (3)
```

1. The **UPDATE** clause names the table to be updated.
2. The **SET** clause names the columns that you are updating and their new values  
   You must update the columns with values that are compatible with the data type fo the column, including **NULL** and **DEFAULT**.
3. The **WHERE** clause specifies the condition a row must meet to be updated. Also called the **search condition**.
   > **Best practices** 
   > The **WHERE** clause should refer to a primary or a foreign key.
   > Before you execute an **UPDATE** statement, you should create a test **SELECT** statement with the same search condition in the **WHERE** clause. If the **SELECT** clause is correct, then you can copy its **WHERE** clause into the **UPDATE** statement.

### Subquery in UPDATE statement
Create a subquery in the **WHERE** clause of an **UPDATE** statement to identify the rows that you want to update.

> **Example**
```sql
UPDATE invoices 
SET terms_id = 1
WHERE vendor_id = 
   (SELECT vendor_id
    FROM vendors
    WHERE vendor_name = 'Pacific Bell');
```
A subquery is used in the **WHERE** clause to identify the invoices that are updated. Returns the vendor_id value for the vendor in the vendors table with the name "Pacific Bell".  
In subqueries, the **SELECT** clause contains a column that the **UPDATE** clause table and the **FROM** subquery clause have in common.

## DELETE
Use the DELETE statement to remove one or more rows from a table. A foreign key constraint may prevent you from deleting a row. If that is the case, you can delete the row only if you delete all child rows for that row first.

```sql
DELETE FROM invoice_line_items  (1)
WHERE invoice_id = 12;          (2)
```
1. **DELETE** clause specifies the name of the table and must include **FROM** keyword 
2. The **WHERE** clause specifies a serch condition that identifies the rows to delete.  
   This row is optional, but you should include it to ensure that you do not delete the entire table.  

> **Best practices** 
> Before you execute an **DELETE** statement, you should create a test **SELECT** statement with the same search condition in the **WHERE** clause. If the **SELECT** clause is correct, then you can copy its **WHERE** clause into the **DELETE** statement.

### Subquery in DELETE statement
To delete a row from the vendors table that has related rows in the invoices table, you must start by deleting the rows in the invoice_line_items table for the vendor's invoices, using a subquery.

```sql
DELETE FROM invoice_line_items  (1)
WHERE invoice_id IN             (2)
   (SELECT invoice_id
   FROM invoices
   WHERE vendor_id = 115);
```
1. **DELETE** clause specifies the name of the table and must include **FROM** keyword 
2. **WHERE** clause uses a subquery to select all invoice IDs for the vendor from the invoices table. Then, the **DELETE** statement deletes all the invoice line items with those IDs.

# Summary queries