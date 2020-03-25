# Conceptual

Relational Databases are made of tables  
Tables are made of rows and columns  
Rows and columns are sometimes called records and fields, respectively 

## Definitions

<dl>
    <dt>Cell</dt>
    <dd>Intersection of the rows and columns</dd>
    <dt>Column</dt>
    <dd>Represents some sort of entity, like the amount of an invoice</dd>
    <dt>Composite primary key</dt>
    <dd>When a primary key uses two or more columns</dd>
    <dt>Constraint</dt>
    <dd>When assigning column attributes, a _constraint_ restricts the type of data that can be stored in a column. For example, <strong>NOT NULL</strong> and <strong>UNIQUE</strong>.</dd>
    <dt>Data type</dt>
    <dd>Determines the type of information that is stored in the column<br>
    Try to assign the data type that minimizes the use of disk storage because that improves the performance of queries later.
    <ul>
    <li>CHAR, VARCHAR</li>
    <li>INT, DECIMAL</li>
    <li>FLOAT</li>
    <li>DATE</li>
    </ul>
    </dd>
    <dt>Foreign key</dt>
    <dd>One or more columns in a table that refer to a primary key in another table (one-to-many relationship)</dd>
    <dt>Index</dt>
    <dd>Provides an efficient way to access data from a table based on the values in specific columns.<br>Created automatically for a tables primary and non-primary keys</dd>
    <dt>Non-primary key</dt>
    <dd>Uniquely identifies each row in the table.</dd>
    <dt>Primary key</dt>
    <dd>Uniqueily identifies each row in the table. Usually a single column, but can be more than 1 column</dd>
    <dt>Referential integrity</dt>
    <dd>Makes sure that any changes to the data in the db do not create invalid relationships between tables.</dd>
    <dt>Row</dt>
    <dd>Contains a set of values for a single instance of the entity </dd>
    <dt>Unique key</dt>
    <dd>MySQL specific, not all dbs let you define one.</dd>
    <dt>Null</dt>
    <dd>Value that is unknown, unavailable, or not applicable.</dd>
    <dt>Default value</dt>
    <dd>Value that is assigned to the column if another value is not provided</dd>
    <dt>Auto increment column</dt>
    <dd>Value is generated automatically by the DBMS</dd>
    <dt>Entity-relationship (ER) or enhanced entity-relationship (EER) diagram</dt>
    <dd>Used to show how the tables in a database are defined and related</dd>
    <dt>Result set/table</dt>
    <dd>the data that is returned by a query</dd>
    <dt>DML (Data Manipulation Language)</dt>
    <dd><p>Statements tha work with the data in a db</p>
    <ul>
    <li>SELECT - gets data from one or more tables</li>
    <li>INSERT - adds new rows to a table</li>
    <li>UPDATE - changes existing rows in a table</li>
    <li>DELETE - deletes existing rows from a table</li>
    </ul>
    </dd>
    <dt>DDL (Data Definition Language)</dt>
    <dd><p>Statements that create databases and work with the objects within a db (usually used by db admins)</p>
    <ul>
    <li>CREATE DATABASE - creates a new db on the server</li>
    <li>CREATE TABLE - creates a new table in a db</li>
    <li>CREATE INDEX - creates a new index for a table</li>
    <li>ALTER TABLE - changes the definition of an existing table</li>
    <li>ALTER INDEX - changes the structure of an existing index</li>
    <li>DROP DATABASE - deletes an existing db and all of its tables</li>
    <li>DROP TABLE - deletes an existing table</li>
    <li>DROP INDEX - deletes an existing index</li>    
    </ul>
    </dd>
    <dt>Database object</dt>
    <dd>Any defined object in a db that is used to store or reference data.<br>
    Anything that is created from a CREATE command is a db object, including:
    <ul>
    <li>Table</li>
    <li>View</li>
    <li>Sequence</li>
    <li>Index</li>
    <li>Synonym</li>
    </ul>
    </dd>
    <dt>Scalar function</dt>
    <dd>A query that operates on a single value and returns a single value</dd>
    <dt>Aggregate function</dt>
    <dd>a query that operates on a series of values and returns a single summary value. Sometimes called <em>column</em> functions because they typically operate on the values in columns.</dd>
    <dt>Summary query</dt>
    <dd>A query that contains one or more aggregate functions.</dd>    

## Building queries 
Best practice to build queries one clause at a time.

# Statements 

<dt>SELECT</dt>
<dd>Names the columns to be retrieved</dd>
<dt>INSERT INTO</dt>
<dd>Names the columns whose values are supplied in the <strong>VALUES</strong> clause</dd>
<dt>VALUES</dt>
<dd>Lists the data that is inserted with an <strong>INSERT</strong> clause</dd>
<dt>UPDATE</dt>
<dd>Changes the data in one or more rows of a table</dd>
<dt>DELETE</dt>
<dd>Deletes one or more rows from a table</dd>
<dt>FROM</dt>
<dd>Names the base table from which the query retrieves the data</dd>
<dt>AS</dt>
<dd>Assigns a new name to a group of columns. The new name is the column alias.<br>Called a calculated value because it exists only in this query<br>When there is a space in the alias name, enclose the alias name in quotes. For example, 'Test Row'</dd>
<dt>WHERE</dt>
<dd>Filters the rows in the base table by the boolean expression that takes a true, false, or NULL value. For example, <strong>WHERE</strong> value > 0.<br>If you omit the <strong>WHERE</strong> clause, all the rows in the base table are returned.</dd>
<dt>IN</dt>
<dd>Used in <strong>WHERE</strong> clause. Compares the value of the test expression with the list of expressions in the IN phrase. If the test expression is equal to one of the expressions in the list, the row is included in the query results and each of the expressions in the list is converted to the same thpe of data as the test expression automatically.</dd>

**Example**:
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
<dt>LIKE or REGEXP</dt>
<dd>Used in the **WHERE** clause. Use to retrieve rows that match a specific string pattern or mask.</dd>

**LIKE Wildcards**:
| Character | Definition | Example | Returns |
|:----------|:-----------|:--------|:--------|
| %         | Matches any string of zero or more characters | **WHERE** vendor_city LIKE 'SAN%' | returns San Diego, Santa Ana |
| _         | Matches any single character | **WHERE** vendor_name LIKE 'COMPU_ER' | Returns Compuserve, Computerworld |

**REGEXP special characters/constructs**
| Character | Definition | Example | Returns |
|:----------|:-----------|:--------|:--------|
| ^         | Matches the pattern to the beginning of the value being tested | **WHERE** vendor_city REGEXP '^SA' | returns Pasadena, Santa Ana |
| $         | Matches the pattern to the end of the value being tested | **WHERE** vendor_city REGEXP 'NA$' | Returns Gardena, Pasadena | .         | Matches any single character |
| [charlist]| Matches any single character listed within the brackets | **WHERE** vendor_city REGEXP 'N[CV]' | Returns NC, NV but not NJ or NY |
| [char1 - char2]| Matches any single character within the given range | **WHERE** vendor_city REGEXP 'N[A-J]' | Returns NC, NV but not NJ or NY |
| \|\ | Separates two string patterns and matches either one | **WHERE** vendor_city REGEXP 'RS|SN' | Returns Trave(rs)e City, Fre(sn)o

**Example**  
**WHERE** vendor_city REGEXP '[A-Z][AEIOU]N$' - returns any vendor_city that ends with any letter, then a vowel, then the letter 'n'





<dt></dt>
<dd></dd>
<dt></dt>
<dd></dd>
<dt></dt>
<dd></dd>
<dt></dt>
<dd></dd>
<dt></dt>
<dd></dd>
<dt></dt>
<dd></dd>
 

**** or **** -  
 
    
    
:

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

**equijoin/equi-join** - When you use the equal operator to join two tables on a common column. 
Common for the columns that are being compared to have the same name.
        
>Example 1:
```sql
SELECT invoice_number, vendor_name
FROM vendors
    JOIN invoices USING (vendor_id) (1)
ORDER BY invoice_number;
```
(1) USING (vendor_id) replaced 'ON vendors.vendor_id = invoices.vendor_id'
        
> Example 2:
```sql
SELECT department_name, last_name, project_number
FROM departments
    JOIN employees USING (department_number)    (1)
    LEFT JOIN projects USING (employee_id)      (2)
ORDER BY department_name;
```
(1) INNER JOIN between departments and employees on the department_number column 
(2) LEFT JOIN between employees and projects using the employee_id column 

## NATURAL keyword 
You don't specific the column that's used to join the two tables. The db joins the two tables based on all columns in the two tables that have the same name.

> Example: 
```sql
SELECT department_name AS dept_name, last_name, project_number
FROM departments
    NATURAL JOIN employees                      (1)
    LEFT JOIN projects USING (employee_id)      (2)
ORDER BY department_name;
```
(1) JOINs departments and employees on columns where they intersect
(2) Creates a LEFT JOIN between employees and projects on employee_id column 

## CROSS JOINs 
Produces a result set that includes each row from the first table joined with each row from the second table. 
Result set is called a Cartesian product 

> Example:
```sql
SELECT departments.department_number, department_name, employee_id, last_name
FROM departments CROSS JOIN employees   (1)
ORDER BY departments.department_number;
```
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
Use aggregate functions that operate on a series of values and return a singe summary value. Sometimes called _column functions_ because they typically operate on the values in columns. A query that contains one or more aggregate functions is typically referred to as a **summary query**.

## Most common aggregate functions
| Function syntax                       | Result      |
| --------------------------------------|-------------|
| AVG([ALL or DISTINCT] expression)     | The average of all non-null values in the expression |
| SUM([ALL or DISTINCT] expression)     | The total of the non-null values in the expression |
| MIN([ALL or DISTINCT] expression)     | The lowest non-null value in the expression |
| MAX([ALL or DISTINCT] expression)     | The highest non-null value in the expression |
| COUNT([ALL or DISTINCT] expression)   | The number of non-null values in the expression |
| COUNT(*)                              | The number of rows selected by the query |

- **ALL** keyword is a default. This includes all values except for null values.
- **COUNT(*)** includes null values
- Use **DISTINCT** if you do not want duplicate values included.
  - Most often, you will use **DISTINCT** with the **COUNT** function. 
  - It does not have an effect on **MIN** or **MAX**

**NOTE**: The expression in the **Result** column is typically just a column name.

**Examples**
```sql
SELECT COUNT(*) AS number_of_invoices,
   SUM(invoice_total - payment_total - credit_total) AS total_due   (1)
FROM invoices
WHERE invoice_total - payment_total - credit_total > 0;             (2)
```
1. **SUM** function calculates the balance due of an invoice using 3 columns and an alias. The result is a single value that represents the total amount due for all the selected invoices.
2. The **WHERE** clause filters these to show where a balance is due.

```sql
SELECT 'After 1/1/2018' AS selection_date,
   COUNT(*) AS number_of_invoices,                      (1)
   ROUND(AVG(invoice_total), 2) AS avg_invoice_amt,     (2)
   SUM(invoice_total) AS total_invoice_amt              (3)
FROM invoices
WHERE invoice_date > '2018-01-01';
```
1. Counts the number of rows that pass the **WHERE** clause filter
2. Calulates the average amount of invoices that pass the **WHERE** clause filter
3. Calcualtes the total amount of invoices that pass the **WHERE** clause filter

```sql
SELECT COUNT(DISTINCT vendor_id) AS number_of_vendors,  (1)
	COUNT(vendor_id) AS number_of_invoices,             (2)
    ROUND(AVG(invoice_total), 2) AS avg_invoice_amt,    (3)
    SUM(invoice_total) AS total_invoice_amt             (4)
FROM invoices
WHERE invoice_date > '2018-01-01';
```
1. Counts the number of vendors that have a unique vendor_id value that also pass the **WHERE** clause filter
2. Counts every invoice that passes the **WHERE** clause filter. This function is used for clarity - you would normally use use **COUNT(*)**.
3. Rounds the average of the invoice_total column to 2 decimal places and uses an alias
4. Sums the invoice_total column as an alias

## GROUP BY and HAVING
The GROUP BY clause determines how the selected rows are grouped, and the HAVING cluase determines which groups are included in the final results. In **GROUP BY**, you can list more than one expression, separated by commas, and they are grouped in ascending sequence.
These clauses are included after the **WHERE** clause and before the **ORDER BY** clause. 

When you use **GROUP BY**, a single row is returned for each unique set of values in the grouped columns. For example, if a result set is grouped by the vendor_id column, only one row is returned for each vendor, and that vendor is summarized by the aggregate functions that are included in the **SELECT** clause.

**Examples**

```sql
SELECT vendor_id, ROUND(AVG(invoice_total), 2) AS average_invoice_amount
FROM invoices
GROUP BY vendor_id                      (1)
HAVING AVG(invoice_total) > 2000        (2)
ORDER BY average_invoice_amount DESC;
```
1. Groups the columns in the **SELECT** clause by vendor_id
2. Specifies a search condition for a group or an aggregate.

```sql
SELECT vendor_name, vendor_state,
   ROUND(AVG(invoice_total), 2) AS average_invoice_amount              (1)
FROM vendors JOIN invoices ON vendors.vendor_id = invoices.vendor_id
GROUP BY vendor_name        (2)
HAVING AVG(invoice_total) > 2000
ORDER BY average_invoice_amount DESC;
```
1. When you have an aggregate in the **SELECT** clause, the aggregate is calculated for each group specified by the **GROUP BY** clause.
2. Groups the columns in the **SELECT** clause by vendor_name

```sql
SELECT vendor_state, vendor_city, COUNT(*) AS invoice_qty,  (1)
   ROUND(AVG(invoice_total), 2) AS invoice_avg              (2)
FROM invoices JOIN vendors
   ON invoices.vendor_id = vendors.vendor_id                (3)
GROUP BY vendor_state, vendor_city                          (4)
HAVING COUNT(*) >= 2                                        (5)
ORDER BY vendor_state, vendor_city;
```
1. Use **COUNT(*)** to count the total number of invoices for each row in the result table
2. Round the average of the invoice total to 2 decimal places and use an alias 
3. **JOIN** the tables on the vendor_id row
4. Group the columns in the **SELECT** clause by vendor_state, then vendor_city
5. The **HAVING** clause filters the result set to include only the state and city groups that have at least 2 invoices

### HAVING clause vs. WHERE clause
**WHERE** clauses are applied to every row. **HAVING** are applied to each group of rows.

**Example**
```sql
SELECT vendor_name,
	COUNT(*) AS invoice_qty,                        (1)
    ROUND(AVG(invoice_total), 2) AS invoice_avg     (2)
FROM vendors JOIN invoices
	ON vendors.vendor_id = invoices.vendor_id
GROUP BY vendor_name                                (3)
HAVING AVG(invoice_total) > 500                     (4)
ORDER BY invoice_qty DESC;
```
1. Calculates an invoice count for the vendor_name column (that is listed in the **GROUP BY** column)
2. Calculates an average invoice amount 
3. Groups the invoices in the invoice table by vendor name
4. Limits the groups in the result set to those that have an average invoice total greater than 500

```sql
SELECT vendor_name,
	COUNT(*) AS invoice_qty,                        (1)
    ROUND(AVG(invoice_total), 2) AS invoice_avg     (2)
FROM vendors JOIN invoices
	ON vendors.vendor_id = invoices.vendor_id
WHERE invoice_total > 500                           (3)
GROUP BY vendor_name                                (4)
ORDER BY invoice_qty;
```
1. Calculates an invoice count for the vendor_name column (that is listed in the **GROUP BY** column)
2. Calculates an average invoice amount 
3. Limits the invoices in the groups to those that have an invoice total greater than 500. This is applied to every row before anything is grouped. 
4. The results of the **WHERE** clause are grouped by vendor_name

**BEST PRACTICE**
You can use either the **WHERE** or **HAVING** clause to code non-aggregte clauses, but it makes more sense to include them all in the **HAVING** clause for readability.

### WITH ROLLUP operator
Use this operator at the end of the **GROUP BY** clause to add one or more summary rows to a result set that uses grouping and aggregates.

**Example**
```sql
SELECT vendor_id, COUNT(*) AS invoice_count,
   SUM(invoice_total) AS invoice_total
FROM invoices
GROUP BY vendor_id WITH ROLLUP;
```
This query adds a summary row to the end of the result set that summarizes all of the aggregate columns in the result set. If a column cannot be summarized, it contains a **NULL** value.

## GROUPING function
Sometimes it is difficult to distinguish between the null values that are due to grouping and the null values that are due to summarizing. This function is commonly used to replace the nulls that are generated by **WITH ROLLUP** with literal values.

The **GROUPING** function returns a 1 if the expression is null because it's in a summary row, and returns 0 otherwise.

```sql
SELECT  IF(GROUPING(invoice_date) = 1, 'Grand totals', invoice_date)    (1)
      AS invoice_date,
   IF(GROUPING(payment_date) - 1, 'Invoice date totals', payment_date)  (2)
      AS payment_date,
   SUM(invoice_total) AS invoice_total,                                 
   SUM(invoice_total - credit_total - payment_total) AS balance_due     
FROM invoices
WHERE invoice_date BETWEEN '2018-07-24' AND '2018-07-31'               
GROUP BY invoice_date, payment_date WITH ROLLUP;
```
1. If the invoice_date column contains a null value because it's in a summary row, 'Grand totals' is displayed in the column.
2. If the payment_date column contains a null value because it's in a summary row, 'Invoice date totals' is displayed in the column.

## Window functions
Similar to **GROUP BY**, except that the groups (or partitions), are not collapsed to a single row - all rows in the result set are returned. 

Think of this as exposing a window of rows to a function.

To start, you code an aggregate window function by including the **OVER** clause. This clause defines the window that's used by the aggregate function.
**OVER()** - uses a single parition. All the rows for that column will be the same value
**OVER(PARTITION BY [column_name])** - partitions the result set by the column parameter. The aggregate function is performed and grouped by each unique value in the specified column.
A **window** consists of all the rows that are needed to evaluate the function for the current row. 

**Example**
```sql
SELECT vendor_id, invoice_date, invoice_total,
   SUM(invoice_total) OVER() AS total_invoices,                     (1)
   SUM(invoice_total) OVER(PARTITION BY vendor_id) AS vendor_total  (2)
FROM invoices
WHERE invoice_total > 5000;
```
1. Uses the **SUM** function to calculate a total of the invoice_total column.
  - The empty **OVER()** clause means that all of the rows in the result set are included in a single partition. This means that the total_invoices column contains the same value for each column, which is the total of all of the invoices in the result set.
  - To calculate the total of all invoices, the **SUM** functino for each row needs a window into all of the other rows in the result set.
2. The **PARTITION BY** clause partitions the result set by the vendor_id column.
  - This means that the sum of the invoice_total column  is calculated for each vendor instead of all of the vendors.
  - To calculate the total of all invoices for each vendor, the **SUM** function for each row needs a window into all the other rows for the same vendor.
  
```sql
SELECT vendor_id, invoice_date, invoice_total,
   SUM(invoice_total) OVER() AS total_invoices,
   SUM(invoice_total) OVER(PARTITION BY vendor_id
      ORDER BY invoice_total) AS vendor_total       (1)
FROM invoices
WHERE invoice_total > 5000;
```
1. When you add an **ORDER BY** clause in the **OVER(PARTITION BY)** clause, the rows within each partition are sorted and the values from one row to the next are cumulative.
  - Includes a **frame**, which is all of the rows from the start of the partition through the current row. 

## Frames

The number of rows before and after the current row (ROW) or a range of values based on the value of the current row (RANGE).

A frame defines a subset of the current partition. Beacuse a frame is relateve to the current row, it can move within a partition as the current row changes.

If you specify just the starting row for a frame, the ending row is the current row. To specify both a sstarting and ending rtow, you use the **BETWEEN clause**. TWhen you use **BETWEEN**, the starting row for a frame must not come after the ending row.

| Value                 | Description                   |
|:----------------------|:-----------------------------
|CURRENT ROW            | The frame starts or ends with the current row.
|UNBOUNDED PRECEDING    | The frame starts or ends with the first row in the partition.
|UNBOUNDED FOLLOWING    | The frame starts or ends with the last row in the partition.
|expr PRECEDING         | With **ROWS**, the frame starts expr rows before the current row. With **RANGE**, the frame starts with the first row before the current row whose value is expr less than the value of the current row.
|expr FOLLOWING         | With **ROWS**, the frame starts expr rows after the current row. With **RANGE**, the frame starts with the last row after the current row whose fvalue is expr greater than the value of the current row.


```sql
SELECT vendor_id, invoice_date, invoice_total,
   SUM(invoice_total) OVER() AS total_invoices,
   SUM(invoice_total) OVER(PARTITION BY vendor_id ORDER BY invoice_date
      ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)     (1)
      AS vendor_total
FROM invoices
WHERE invoice_date BETWEEN '2018-04-01' AND '2018-04-30';
```
1. Selects the rows between the frist row in the partion and the current row.

**peer** - a row that has the same value as other rows in the sort column. 

The following example 
```sql
SELECT vendor_id, invoice_date, invoice_total,
   SUM(invoice_total) OVER() AS total_invoices,
   SUM(invoice_total) OVER(PARTITION BY vendor_id ORDER BY invoice_date
   RANGE BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)                       (1)
         AS vendor_total
FROM invoices
WHERE invoice_date BETWEEN '2018-04-01' AND '2018-04-30';
```
1. This frame includes all of the rows within the partition, along with the current row and any of its peers. 

The following example calculates the 3-month avergage of the sum of invoice totals.

```sql
SELECT MONTH(invoice_date) AS month, SUM(invoice_total) AS total_invoices,
   ROUND(AVG(SUM(invoice_total)) OVER(ORDER BY MONTH(invoice_date)
      RANGE BETWEEN 1 PRECEDING AND 1 FOLLOWING), 2) AS 3_month_avg         (1)
FROM invoices
GROUP BY MONTH (invoice_date);
```
1. Uses **RANGE** and indicates the the current month, 1 month before, and 1 month after should be used to calculate the average. If there is no preceding or subsequent row, then just the available rows are used to calculate the average.

## Named windows

In some cases, you may need to code a **SELECT** statement with two or more aggregate functions that use the same window. If so, then you may want to use a **named window** so that you don't have to repeat the definition for the window for each function. 

Use a **WINDOW** clause after the **HAVING** clause and before the **ORDER BY**, when included.  

Similar to using an alias for a column name.

```sql
SELECT vendor_id, invoice_date, invoice_total,
   SUM(invoice_total) OVER vendor_window AS vendor_total,           (2)
   ROUND(AVG(invoice_total) OVER vendor_window, 2) AS vendor_avg,   (2)
   MAX(invoice_total) OVER vendor_window AS vendor_max,             (2)
   MIN(invoice_total) OVER vendor_window AS vendor_min              (2)
FROM invoices
WHERE invoice_total > 5000
WINDOW vendor_window AS (PARTITION BY vendor_id);           (1)
```
1. Paritions the rows in the result set by the vendor_id column.
2. Applies the partition defined in the **WINDOW** clause to each **OVER** clause

# Subqueries
A **SELECT** statement that is coded within another SQL statement. It is used to create queries that work with two or more tables. A subquery cannot include an **ORDER BY** clause.

## 4 ways to introduce a subquery in a SELECT statement
1. In a **WHERE** clause as a search condition
2. In a **HAVING** clause as a search condition
3. In the **FROM** clause as a table specification.
4. In the **SELECT** clause as a column specification.

**Example**

The following statement returns all the invoices from the invoices table that have invoice totals greater than the average of all the invoices.

```sql
SELECT invoice_number, invoice_date, invoice_total
FROM invoices
WHERE invoice_total >               (2)
   (SELECT AVG(invoice_total)       (1)
   FROM invoices)
ORDER BY invoice_total;
```
1. The suqeiry calculates the average of all the invoices
2. The search condition testes each invoice to see if its invoice total is greater than that average.

## When to use subqueries (vs JOINS)

Most subqueries can be restated as JOINS, and vice versa. When you use a subquery in a **WHERE** clause, its results cannot ve included in the final set because it is not included in the **FROM** clause.

**JOIN**
- THE **SELECT** clause of a join can include columns from both tables.
- A JOIN is generally more intuitive when it uses an existin relationship between the two tables, such as a primary key to foreign key relationship.

```sql
SELECT invoice_number, invoice_date, invoice_total
FROM invoices JOIN vendors 
   ON invoices.vendor_id = vendors.vendor_id
WHERE vendor_state = 'CA'
ORDER BY invoice_date;
```

**Subquery**
- You can use a subquey to pass an aggregate value to the main query.
- A subquery tends to be more intuitive when it uses an ad hoc relationship between the two tables.
- Long, complex queries can sometimes be easier to code using subqueries.

```sql
SELECT invoice_number, invoice_datte, invoice_total
FROM invoices 
WHERE vendor_id IN
   (SELECT vendor_id                (1)
   FROM vendors
   WHERE vendor_state = 'CA')
ORDER BY invoice_date;
```
1. You cannot include a column name from the vendors table because it is not in the **FROM** clause, it is in the subquery.

## Subqueries in the WHERE clause
Use the **IN** ooerator to test whetehr an expression is contained in a list of values. You can provide that list of values in  a subquery.  

When you use the **IN** operator with a subquery, the subquery must return a single column that provides the list of values. Statements that use the **IN** operator with a subquery can usually be restated as an **OUTER JOIN**.

```sql
SELECT vendor_id, vendor_name, vendor_state
FROM vendors
WHERE vendor_id NOT IN              (2)
   (SELECT DISTINCT vendor_id       (1)
   FROM invoices)
ORDER BY vendor_id;
```
1. Returns a list of each vendor that is in the invoices table.
2. Returns data about the vendors whose IDs are not in that list.

## Comparison operators and subqueries
When you use a comparison operator to return a single value, you need to use an aggregate function.
```sql
SELECT invoice_number, invoice_date,
   invoice_total - payment_total - credit_total AS balance_due
FROM invoices
WHERE invoice_total - payment_total - credit_total > 0
  AND invoice_total - payment_total - credit_total < 
      (
         SELECT AVG(invoice_total - payment_total - credit_total)
         FROM invoices
         WHERE invoice_total - payment_total - credit_total > 0
      )
ORDER BY invoice_total DESC;
```

## ALL keyword
Returns a boolean. Used to modify the comparison operator so that the condition must be true for all the values retuned by a subquery. If no rows are returned by the subqeuery, a comparison that uses the **ALL** keyword is always true.

| Condition      | Equivalent expression | Description       |
|:---------------|:----------------------|:------------------|
|x > ALL (1, 2)  | x > 2                 | Evaluates to true if x is greater than the maximum value returned by the subquery.|
|x < ALL (1, 2)  | X < 1                 | Evaluates to true if x is less than the minimum value returned by the subquery.|
| x = ALL (1, 2) | (x = 1) AND (x = 2)   | Evaluates to true if the subquery returns a single value that is equal to x of if the subquery returns multiple values that are the same and these values are all equal to x |
| x <> ALL (1, 2) | x NOT IN (1, 2)      | Evaluates to true if x is not one of the values returned by a subquery |

**Example**
Return invoices larger than the largest invoice or vendor 34
```sql
SELECT vendor_name, invoice_number, invoice_total
FROM invoices i JOIN vendors v ON i.vendor_id = v. vendor_id
WHERE invoice_total > ALL       (2)
   (SELECT invoice_total        (1)
    FROM invoices
    WHERE vendor_id = 34)
ORDER BY vendor_name;
```
1. Returns the invoice_total column from vendor 34
2. Where the invoice_total is greater than any value returned in the subquery.

## ANY and SOME keywords
Used to test whether a comparison is true for any of the values returned by a subquery. These keywords are interchangeable. 

**Example**
```sql
SELECT vendor_name, invoice_number, invoice_total
FROM invoices i JOIN vendors v ON i.vendor_id = v. vendor_id
WHERE invoice_total < ANY       (2)
   (SELECT invoice_total        (1)
    FROM invoices
    WHERE vendor_id = 115)
```
1. Returns the invoice_total column from vendor 115
2. Where the invoice_total value is less than any of the columns returned in the **ANY** subquery.

This subquery could and should be rewritten using the **MAX** function:
```sql
WHERE invoice_total <        
   (SELECT MAX(invoice_total)
    FROM invoices
    WHERE vendor_id = 115)
```

## Correlated subqueries

**Uncorrelated** subquery is executed once for the entire query.  
**Correlated** subquery is executed once for each row that's processed by the main query. This is similar to looping over a series of values.

**Example**
Retrieves rows from the invoices table for those invoices that have an invoice total that's greater than the average of all the invoices for the same vendor.  
Goes through each vendor_id on the invoice table and calcs the average invoice total where the vendor_id is equal to the vendor_id that is currently being evaluated in the original clause.

```sql
SELECT vendor_id, invoice_number, invoice_total
FROM invoices i
WHERE invoice_total > 
   (SELECT AVG(invoice_total)           (2)
    FROM invoices
    WHERE vendor_id = i.vendor_id)      (1) 
ORDER BY vendor_id, invoice_total;
```
1. Refers to the vendor_id value of the main query.
2. Returns the average of the invoice_total column from the invoice table where the vendor_id is equal to the vendor_id for the column it is querying.  
It does this for each row in the column and compares 
# FIGURE THIS OUT

## EXISTS operator
Tests whether the subquery returns a result set (if it exists or not). Typically used with a correlated subquery.

```sql
SELECT vendor_id, vendor_name, vendor_state
FROM vendors
WHERE NOT EXISTS                            (2)
   (SELECT *                                (1)
    FROM invoices
    WHERE vendor_id = vendors.vendor_id)
```
1. Selects all invoices that have the same vendor_id as the current vendor in the outer query.
2. Uses **NOT EXISTS** to test whether any invoices were found for the current vendor. If not, then the vendor row is included in the result set.

## Subqueries in the HAVING clause
Specify a search condition just like the **WHERE** clause.

## Subqueries in the SELECT clause
Replace a column specification with a subquery. The result of a query must return a single value for that column. In most cases, you use a correlated subquery in the **SELECT** clause.  
You can usually restate each as a **JOIN**, so subqueries are not usually used in **SELECT** clause.

```sql
SELECT vendor_name,
   (SELECT MAX(invoice_date) FROM invoices              (1)
    WHERE vendor_id = vendors.vendor_id) AS latest_inv
FROM vendors
ORDER BY latest_inv DESC;
```
1. Calculates the maximum invoice date for each vendor in the vendors table by referring to the vendor_id from the vendors table in the **FROM** clause of the main query.  
Goes through each vendor_id in the invoices table and calculates the max date for each vendor_id in the vendors table.

**Restated as a JOIN**
```sql
SELECT vendor_name, MAX(invoice_date) AS latest_inv
FROM vendors v
   LEFT JOIN invoices i ON v.vendor_id = i.vendor_id
GROUP BY vendor_name
ORDER BY latest_inv DESC;
```

## Subqueries in the FROM clause
Code a subquery in place of a table specification. The result is sometimes referred to as an _inline view_.  
When you code a subquery in the **FROM** clause, you must assign an alias.  
In the subquery, you should use an alias for any columns in the subquery that perform calculations. The main query can refer to the columns by these names.

**Example**

Returns the largest invoice total for the top vendor in each state.

```sql
SELECT vendor_state, MAX(sum_of_invoices) AS max_sum_of_invoices    (2)
FROM 
(
   SELECT vendor_state, vendor_name,            (1)
      SUM(invoice_total) AS sum_of_invoices     (2)
   FROM vendors v JOIN invoices i
         ON v.vendor_id = i.vendor_id
   GROUP BY vendor_state, vendor_name
) t                                             (3)
GROUP BY vendor_state
ORDER BY vendor_state;
```
1. The subquery returns the sum of the invoice_total for every vendor that is in the invoices table
2. Alias in the subquery is used in the main query.
3. Alias for the subquery 

## Complex queries with subqueries

The following query retrieves the vendor from each state that has the largest invoice total. It uses 3 subqueries as outlined in the comments.

```sql
SELECT t1.vendor_state, vendor_name, t1.sum_of_invoices
FROM
   (
      -- 1. invoice totals by vendor
      SELECT vendor_state, vendor_name,
         SUM(invoice_total) AS sum_of_invoices
      FROM vendors v JOIN invoices i
         ON v.vendor_id = i.vendor_id
      GROUP BY vendor_state, vendor_name
   ) t1
   JOIN
      (
         -- 2. top invoice totals by state
         SELECT vendor_state,
            MAX(sum_of_invoices) AS sum_of_invoices
         FROM
         (
            -- 3. invoice totals by vendor
            SELECT vendor_state, vendor_name,
               SUM(invoice_total) AS sum_of_invoices
            FROM vendors v JOIN invoices i
               ON v.vendor_id = i.vendor_id
            GROUP BY vendor_state, vendor_name
         ) t2
         GROUP BY vendor_state
      ) t3
   ON t1.vendor_state = t3.vendor_state AND
      t1.sum_of_invoices = t3.sum_of_invoices
ORDER BY vendor_state;
```
### Procedure for building complex queries
1. State the problem that you want to solve in plain English.
  - Which vendor in each state has the largest invoice total?
2. Use pseudocode to outline the query.
```sql
SELECT vendor_state, vendor_name, sum_of_invoices
FROM (subquery returning vendor_state, vendor_name, sum_of_invoices)
JOIN (subquery returning vendor_state, largest_sum_of_invoices)
   ON vendor_state AND sum_of_invoices
ORDER BY vendor_state;
```
3. Code the subqueries and test them to be sure that they return the correct data.
  - Code the first subquery:
```sql
SELECT vendor_state, vendor_name, SUM(invoice_total) AS sum_of_invoices
FROM vendors v JOIN invoices i
   ON v.vendor_id = i.vendor_id
GROUP BY vendor_state, vendor_name
```
  - Code the second subquery:
```sql
SELECT vendor_state, MAX(sum_of_invoices) AS sum_of_invoices
FROM
(
   SELECT vendor_state, vendor_name,
      SUM(invoice_total) AS sum_of_invoices
   FROM vendors v JOIN invoices i
      ON v.vendor_id = i.vendor_id
   GROUP BY vendor_state, vendor_name
) t
GROUP By vendor_state
```
4. Code and test the final query.

## Common table expressions (CTE)
A CTE is a **SELECT** statement that creates one or more named temporary result sets that can be used by the query that follows. Use CTEs to simplify complex queries that use subqueries.  
 - CTEs begin with the **WITH** keyword, followed bgy the definition of the CTE. Then, you code the statement that uses it.  
 - When you use multiple CTEs, separate them with columns.  
 - You can use them with **SELECT**, **INSERT**, **UPDATE**, and **DELETE** clauses, but they are most often used with **SELECT**.

```sql
WITH summary as
(
   SELECT vendor_state, vendor_name, SUM(invoice_total) AS sum_of_invoices
   FROM vendors v JOIN invoices i 
      ON v.vendor_id = i.vendor_id
   GROUP BY vendor_state, vendor_name
),
top_in_state AS 
(
   SELECT vendor_state, MAX(sum_of_invoices) AS sum_of_invoices
   FROM summary
   GROUP BY vendor_state
)
SELECT summary.vendor_state, summary.vendor_name,
      top_in_state.sum_of_invoices
FROM summary JOIN top_in_state
   ON summary.vendor_state = top_in_state.vendor_state AND
      summary.sum_of_invoices = top_in_state.sum_of_invoices
ORDER BY summary.vendor_state;
```

## Recursive CTEs
A _recursive query_ is a query that is able to loop through a result set and perform processing to return a final result set.
- Commonly used to return hierarchical data such as an organiational chart in which a parent element may have one or more child elements, and each child element may have one or more child elements.

```sql
WITH RECURSIVE employees_cte AS
(
         -- Nonrecursive query
         SELECT employee_id,
            CONCAT(first_name, ' ', last_name) AS employee_name,
            1 AS ranking
         FROM employees
         WHERE manager_id is NULL
      UNION ALL
         -- Recursive query
         SELECT employees.employee_id,
            CONCAT(first_name, ' ', last_name),
            ranking + 1
         FROM employees
            JOIN employees_cte
            ON employees.manager_id = employees_cte.employee.id
)
SELECT *
FROMM employees_cte
ORDER BY ranking, employee_id;
```

# Data types
A **data type** specifies the kind of information the column is inteded to store. This determines the operations that can be performed on the column.

## Data type table

| Category      | Description    |
|:--------------|:---------------|
| Character     | Strings of character data |
| Numeric       | Numbers that don't include a decimal point (integers) and numbers that include a decimal point (real numbers) |
| Date and time | Dates, times, or both |
| Large Object (LOB) | Large string of character or binary data |
| Spatial       | Geographical values |
| JSON          | JSON documents |

## Character types

The two most common character data types are **CHAR** and **VARCHAR**.

| Type      | Bytes         | Description   |
|:----------|:--------------|:--------------|
| CHAR (M)  | Mx4           | Fixed-length strings of character data where M is the number of characters, between 0 and 255. With the utf8mb4 character set, MySQL must reserve four bytes for each character in a CHAR column becuase that's the maximum possible length. |
| VARCHAR (M) | L+1     | Variable-length strings of character data where M is the maximum number of characters, between 0 and 255. For English and Latin characters, the number of bytes used to store the string is equal to length of the string (L) pluse 1 byte to record its length |

## How the character types work with utf8mb4

utf8mb4 character set uses up to 4 bytes to store each character, so its called a multiple-byte character set. When it is used with CHAR, it uses 4 bytes per character. With VARCHAR, it uses 1 byte per character and 1 byte to store its location.

| Data type     | Original value    | Value stored      | Bytes used    |
|:--------------|:------------------|:------------------|:--------------|
| CHAR(2)       | 'CA'              | 'CA'              | 8             |
| CHAR(10)      | 'CA'              | 'CA        '      | 40            |
| VARCHAR(10)   | 'CA'              | 'CA'              | 3             |
| VARCHAR(20)   | 'California'      | 'California'      | 11            |
| VARCHAR(20)   | 'New York'        | 'New York'        | 9             |
| VARCHAR(20)   | 'Ryan's MySQL'    | 'Ryan's MySQL'    | 13            |

### CHAR 
- Stores fixed-length strings.
- Any data stored using this data type always occupies the same number of bytes regardless of the actual length of the string.
- Typically used to define columns that have a fized number of characters, for example, a state column 
- If two characters are stored in a column defined as CHAR(5), then 3 additional spaces are stored after the two characters becuase it is a fixed-length data type.

### VARCHAR
- Stores variable-length strings
- Data stored with this type occupies only the number of bytes needed to store the string plus an extra byte to store the length of the string
- Typically used to define columns whose lengths vary from one row to the next. 

## Integer types

These are positive or negative numbers that don't include a decimal point. The INT type is most commonly used because it can store a wide range of nunbers and only requires 4 bytes of storage.

| Type      | Bytes      |
|:----------|:----------:|
| BIGINT    | 8          |
| INT       | 4     |
| MEDUIMINT | 3     |
| SMALLINT  | 2     |
|TINYINT    | 1     |

**UNSIGNED** - attribute for an integer type to prevent negative values from being stored in the column.
**ZEROFILL** - attribute that sets the **UNSIGNED** attribute automatically, and the integer is displayed with zeros padded from the left, up to the maximum display size. (max display size for INT is 10)
**BOOLEAN** and **BOOL** - synonym for **TINYINT(1)**. 0 is FALSE, 1 is TRUE.

## Fixed-point and floating-point types


### Fixed-point type
| Type      | Bytes     | Description |
|:----------|:---------:|:-------|
| DECIMAL(M, D) | Vary  |Fixed-precision numbers where M specifies the maximum number of total digits (the precision) and D specifies the number of digits to the right of the decima. (the scale). M can range from 1 to 65. D can range from 0 to 30 but can't be larger than M. The defalut is 0. |

### Floating-point type
| Type      | Bytes     | Description |
|:----------|:---------:|:-------|
| DOUBLE    | 8         | Double-precision floating-point numbers |
| FLOAT     | 4         | Single-precision floating-point numbers |

## Date and time types

Typically use TIMESTAMP to track when a row was inserted or last updated.

| Type      | Bytes     | Description |
|:----------|:---------:|:-------|
| DATE      | 3         | Dates from Jan 1, 1000 - Dec 31, 9999. The default format is 'yyyy-mm-dd' |
| TIME      | 3         | Times in the range of -839:59:59 to 839:59:59. The default format is 'hh:mm:ss'. |
| DATETIME  | 8         | Combination date and time from midnight Jan 1, 1970 - Dec 31, 9999. The default format is 'yyyy-mm0dd hh:mm:ss'. |
| TIMESTAMP | 4         | Combination date and time from midnight Jan 1, 1970 - the year 2037. The default format is 'yyyy-mm0dd hh:mm:ss'. |
| YEAR[(4)] | 1         | Years in 4-digit foramt. Allowable values are from 1901 - 2155 |

- Year - entries with 1 and 2-digit entries are acceptable, but converted to 4-digit automatically.

## ENUM and SET types

Both types allow you to restrict the values for a column to a limited set of strings. 

| Type      | Bytes     | Description |
|:----------|:---------:|:-------|
| ENUM      | 1-2       | Stores one value selected from a list of acceptable values. |
| SET       | 1-8       | Stores zero or more values selected from a list of acceptable values | 

- **ENUM** can store only one member in a set of values
- **SET** can store 0, 1, or up to 64 different values

## The large object types

These are designed to store large amounts of binary or character data.  
**BLOB** types (binary large object) store strings of binary data. This data is often used to stroe images, sounds, and video.  
**TEST** types store strings of characters and are sometimes referred to as character large object (CLOB) types.

## Data conversion 
Automatic conversions are called **implicit conversions**.

## CAST AND CONVERT functions

Use the **CAST** and **CONVERT** functions to conver an expression to the data type that you specify.

| Cast type     | Description       |
|:--------------|:------------------|
| CHAR[(N)]     | A string of characters where N is the maximum number of characters. |
| DATE          | A DATE value  |
| DATETIME      | A DATETIME value |
| TIME          | A TIME value      |
| SIGNED [INTEGER] | A signed IN value. The INTEGER keyword is optional |
| UNSIGNED [INTEGER] | An unsigned IN value. The INTEGER keyword is optional |
| DECIMAL[(M[,D])]  | A DECIMAL value where M specifies the precision and D specified the scale. |

### CAST
```sql
SELECT invoice_id, invoice_date, invoice_total,
   CAST(invoice_date AS CHAR(10)) AS char_date,
   CAST(inoice_total AS SIGNED) AS integer_total
FROM invoices;
```

### Explicitly cast string as an integer
```sql
SELECT *
FROM string_example
ORDER BY CAST(emp_id AS SIGNED);
```

### Implicity cast string as an integer
```sql
SELECT *
FROM string_example
ORDER BY emp_id + 0;

### CONVERT
```sql
SELECT invoice_id, invoice_date, invoice_total,
   CONVERT(invoice_date AS CHAR(10)) AS char_date,
   CONVERT(inoice_total AS SIGNED) AS integer_total
FROM invoices;
```

### FORMAT and CHAR functions

**FORMAT** converts a number to a string of characters. This makes large numbers easier to read. Additionally, it rounds the last number.  

**CHAR** returns a binary string for each specified integer. This is typically used to output ASCII control characters that cannot be typed on your keyboard.

| Function                  | Description       |
|:--------------------------|:------------------|
| FORMAT(number, decimal)   | Converts the specified number to a character string with grouped digits separated by commas, rounded to the specified number of decimal digits. If decimal is zero, then the decimal point is omitted. |
| CHAR(value1[,value2]...)  | Converts one or more numbers to a binary string. Each number is interpreted as an integer between 0 and 255. |

# Functions
This section contains common functions and their uses.

## Parsing a string

### Use SUBSTRING_INDEX to parse a string

```sql
SELECT emp_name
   SUBSTRING_INDEX(emp_name, ' ', 1) AS first_name,      1)
   SUBSTRING_INDEX(emp_name, ' ', -1) AS last_name     (   )
FROM string_sample;
```
1. Returns all characters from the start of the string in the emp_name column up to the first space in that column.
2. Returns all characters from the end of the string in the emp_name column up to the last space in that column.

### Use LOCATE to find a character in a string
```sql
SELECT emp_name,
   LOCATE(' ', emp_name) AS first_space,                                (1)
   LOCATE(' ', emp_name, LOCATE(' ', emp_name) + 1) AS second_space     (2)
FROM string_sample
```
1. Returns an integer value for the location of the first space.
2. Returns the location of the second space. This uses a nested LOCATE to start the search at the character after the first space.

### Use SUBSTRING to parse a string
```sql
SELECT emp_name,
   SUBSTRING(emp_name, 1, LOCATE(' ', emp_name) -1) AS first_name       (1)
   SUBSTRING(emp_name, LOCATE(' ', emp_name) +1) AS last_name           (2)
FROM string_sample
```
1. Returns all characters from the beginning of the string to the first space. 
2. Returns all characters after the efirst space to the end of the string.

## Numeric data

|Function                   | Result        |
|:--------------------------|:-------------:|
| ROUND(12.49, 0)           |  12   |
| ROUND(12.50, 0)           | 13    |   
| ROUND(12.49, 1)           | 12.5    | 
| TRUNCATE(12.51, 0)        | 12    |
| TRUNCATE(12.49, 1)        | 12.4  |
| | |
| CEILING(12.5)             | 13    |
| CEILING(-12.5)            | -12   |
| FLOOR(-12.5)              | -13   |
| FLOOR(12.5)               | 12    |
| ABS(-1.25)                | 1.25  |
| ABS(1.25)                 | 1.25  |
| SIGN(-1.25)               | -1    |
| SIGN(1.25)                | 1     |
| | |
| SQRT(125.43)              | 11.1995535... |
| POWER(9, 2)               | 81    |
| | |
| RAND()                    | 0.2444132... |

## Searching for floating-point numbers

You don't/can't search for exact numbers because floats and decimals are approximate numbers.

```sql
SELECT * 
FROM float_sample
WHERE float_value BETWEEN 0.99 AND 1.01
```

Or, you can search for values that round to an exact value:

```sql
SELECT *
FROM float_sample
WHERE ROUND(float_value, 2) = 1.00;
```

## Working with date/time data

|Function                   | Description   |
|:--------------------------|:--------------|
| NOW()<br>SYSDATE()<br>CURRENT_TIMESTAMP() | Returns the current local date and time bsaed on the system's clock. |
| CURDATE()<br>CURRENT_DATE() | Returns the current local date. |
| CURTIME()<br>CURRENT_TIME() | Returns the current local time. |
| UTC_DATE()  | Returns the current date in Greenwich Mean Time (GMT) |
| UTC_TIME()    | Returns the current time in Greenwich Mean Time (GMT) |

### Date/time parsing functions

|Function                   | Result        |
|:--------------------------|:-------------:|
| DAYOFMONTH('2018-12-03')  | 3     |
| MONTH('2018-12-03')       | 12    |
| YEAR('2018-12-03')        | 2018  |
| HOUR('11:35:00')          | 11    |
| MINUTE('11:35:00')        | 35    |
| SECOND('11:35:00')        | 0     |
| DAYOFWEEK('2018-12-03')   | 2     |
| QUARTER('2018-12-03')     | 4     |
| DAYOFYEAR('2018-12-03')   | 337   |
| WEEK('2018-12-03')        | 48    |
| LAST_DAY('2018-12-03')    | 31    |
| | |
| DAYNAME('2018-12-03')     | Monday    |
| MONTHNAME('2018-12-03')   | December  |

## EXTRACT function with date/time

Use **EXTRACT** with any of the date/time units followed by the **FROM** keyword and a date/time value to extract the specified unit from the date/time value and retun an integer value that corresponds to that unit.

|Function                   | Result        |
|:--------------------------|:-------------:|
| EXTRACT(SECOND FROM '2018-12-03 11:35:00') |   0  |
| EXTRACT(MINUTE FROM '2018-12-03 11:35:00') |  35    |
| EXTRACT(HOUR FROM '2018-12-03 11:35:00') |  11    |
| EXTRACT(DAY FROM '2018-12-03 11:35:00') |   3   |
| EXTRACT(MONTH FROM '2018-12-03 11:35:00') |  12    |
| EXTRACT(YEAR FROM '2018-12-03 11:35:00') |   2018   |
| EXTRACT(MINUTE_SECOND FROM '2018-12-03 11:35:00') |  3500    |
| EXTRACT(HOUR_MINUTE FROM '2018-12-03 11:35:00') |  1135    |
| EXTRACT(DAY_HOUR FROM '2018-12-03 11:35:00') |   311   |
| EXTRACT(YEAR_MONTH FROM '2018-12-03 11:35:00') |  201812    |
| EXTRACT(HOUR_SECOND FROM '2018-12-03 11:35:00') |   113500   |
| EXTRACT(DAY_MINUTE FROM '2018-12-03 11:35:00') |  31135    |
| EXTRACT(DAY_SECOND FROM '2018-12-03 11:35:00') |  3113500    |

## Formatting dates and times

### Common codes for date/time format strings

|Function                   | Result        |
|:----------|:--------------|
| %m        | Month, numeric (01...12)   |
| %c        | Month, numeric (1...12)   |
| %M        | Month name (January...December)   |
| %b        | Abbreviated month name (Jan...Dec)    |
| %d        | Day of the month, numeric(00...31)    |
| %e        | Day of the month, numeric(0...31) |
| %D        | Day of the month with suffix(1st, 2nd, 3rd, etc)  |
| %y        | Year, numeric, 2 digits |
| %Y        | Year, numeric, 4 digits   |
| %W        | Weekday name (Sunday...Saturday)  |
| %a        | Abbreviated weekday name (Sun...Sat) |
| %H        | Hour(00...23) |
| %k        | Hour(0...23)  |
| %h        | Hour(01...12) |
| %l        | Hour(1...12)  |
| %i        | Minutes (00...59) |
| %r        | Time, 12-hour (hh:mm:ss AM or PM) |
| %T        | Time, 24-hour (hh:mm:ss)  |
| %S        | Seconds (00...59)     |
| %p        | AM or PM  |

### Examples
|Function                   | Result        |
|:--------------------------|:-------------:|
| DATE_FORMAT('2018-12-03', '%m/%d/%y') |     12/03/2018  |
| DATE_FORMAT('2018-12-03', '%W, %M, %D, %Y') |     Monday, December 3rd, 2018  |
| DATE_FORMAT('2018-12-03', '%e-%b-%y') |     3-Dec-18  |
| DATE_FORMAT('2018-12-03 16:45', '%r') |     04:45:00 PM  |
| DATE_FORMAT('16:45', '%r') |     04:45:00 PM  |
| DATE_FORMAT('16:45', '%l:%i %p') |     4:45 PM  |

### Performing calculations with date/time

|Function                   | Result        |
|:--------------------------|:--------------|
| DATE_ADD('2018-12-31', INTERVAL 1 DAY)    | 2019-01-01 |
| DATE_ADD('2018-12-31', INTERVAL 3 MONTH)    | 2019-03-31 |
| DATE_ADD('2018-12-31 23:59:59', INTERVAL 1 SECOND)    | 2019-01-01 00:00:00 |
| DATE_ADD('2019-01-01', INTERVAL -1 DAY)    | 2018-12-31 |
| DATE_SUB('2018-12-31', INTERVAL 1 DAY)    | 2018-12-31 |
| DATE_ADD('2016-02-29', INTERVAL 1 YEAR)    | 2017-02-28 |
| DATE_ADD('2018-02-29', INTERVAL 1 YEAR)    | NULL |
| DATE_ADD('2018-12-31 12:00', INTERVAL '2 12' DAY_HOUR)    | 2019-01-03 00:00:00 |
| | |
| DATEDIFF('2018-12-30', '2018-12-03)    | 27 |
| DATE_ADD('2018-12-31 23:59:59', '2018-12_03')    | 27 |
| DATE_ADD('2018-12-03', '2018-12-30')    | -27 |
|  |  |
| TO_DAYS('2018-12-30') - TO_DAYS('2018-12-03)    | 27 |
| TIME_TO_SEC('10:00') - TIME_TO_SEC('09:59')    | 60 |

## Searching for a date

### Search for a range of dates
```sql
SELECT *
FROM date_sample
WHERE start_date >= '2018-02-28' AND start_date < '2018-03-01';
```

### Search for month, day, and year integers

```sql
SELECT * 
FROM date_sample
WHERE MONTH(start_date) = 2 AND
   DAYOFMONTH(start_date) = 28 AND
   YEAR(start_date) = 2018;
```

### Search for a formatted date
```sql
SELECT * 
FROM date_sample
WHERE DATE_FORMAT(start_date, '%m-%d-%Y') = '02-28-2018';
```

## Searching for a time

### Search for a time that has been formatted
```sql
SELECT * FROM date_sample
WHERE DATE_FORMAT(start_date, '%T') = '10:00:00'
```

### Search for a time that hasn't been formatted
```sql
SELECT * FROM date_sample
WHERE EXTRACT(HOUR_SECOND FROM start_date) = 100000;
```

### Search for an hour of the day
```sql
SELECT * FROM date_sample
WHERE HOUR(start_date) = 9;
```

### Search for a range of times
```sql
SELECT * FROM date_sample
WHERE EXTRACT(HOUR_MINUTE FROM start_date) BETWEEN 900 AND 1200;
```

## CASE function

Returns a value that's determined by the conditions you specify. When MySQL finds an expression in a **WHEN** clause that's equal to the input expression, it returns the expression specified in the matching **THEN** clause.

**Example**

The following example determines the status fo the invoices in the invoices table.

```sql
SELECT invoice_number, invoice_total, invoice_date, invoice_due_date,
   CASE
      WHEN DATEDIFF(NOW(), invoice_due_date) > 30
         THEN 'Over 30 days past due'
      WHEN DATEDIFF(NOW(), invoice_due_date) > 0
         THEN '1 to 30 days past due'
      ELSE 'Current'
   END AS invoice_status
FROM invoices
WHERE invoice_total - payment_total - credit_total > 0;
```

## IF, IFNULL, COALESCE functions

### IF function
Use the **IF** function to test a conditino and return one value if the condition is true or another value if the condition is false.
```sql
SELECT vendor_name,
   IF(vendor_city = 'Fresno', 'Yes', 'No') AS is_city_fresno
FROM vendors;
```
### IFNULL function

Allows you to substituted non-null values for null values. The following example returns the first expression if it isn't null. Otherwise, it returns the replacement value you specify. 

```sql
SELECT payment_date,
   IFNULL(payment_date, 'No Payment') AS new_date
FROM invoices;
```
### COALESCE function

Allows you to substituted non-null values for null values from a list of values. Returns the first expression in the list that isn't null. If all of the expressions are null, this functionreturns a null value.

```sql
SELECT payment_date,
   COALESCE(payment_date, 'No Payment') AS new_date
FROM invoices;
```

## Regular expression functions

Use a string pattern to search a string expression.

| Function | Example | Result | Description |
|:---------|:-------|:------------|:------------|
| REGEXP_LIKE(expr, pattern) | REGEXP_LIKE('abc123', '123') | 1 | Returns 1 (true) if the string expression matches the pattern. Otherwise, returns 0 (false). |
| REGEXP_LIKE(expr, pattern)| REGEXP_LIKE('abc123', '^123') | 0 | |
| REGEXP_INSTR(expr, pattern[, start]) | REGEXP_LIKE('abc123', '123') | 4 | Returns the index of the first character of the substring in the string expression that matches the pattern, starting at the specified start position. If the startposition is omitted, the search starts at the beginning of the string. If the pattern ins't found, the function returns 0. |
| REGEXP_SUBSTR(expr, pattern[, start]) | REGEXP_SUBSTR('abc123', '[A-Z][1-9]*$') | c123 | Returns the first substring of the string expression that matches thepattern starting at the specified position. If the start position is omitted, the first substring is returned. If the pattern isn't found, the function returns a null value. |
| REGEXP_REPLACE(expr, pattern, replace[,start] | REGEXP_REPLACE('abc123', '1|2', '3') | abc333 | Returns the string expression with all occurrences of the pattern repaced with the replace string. |

### REGEXP_INSTR function

```sql
SELECT DISTINCT vendor_city, REGEXP_INSTR(vendor_city, ' ') AS space_index
FROM vendors
WHERE REGEXP_INSTR(vendor_city, ' ') > 0
ORDER BY vendor_city;
```

### REGEXP_SUBSTR function

```sql
SELECT vendor_city, REGEXP_SUBSTR(vendor_city, '^SAN|LOS') AS city_match
FROM vendors
WHERE REGEXP_SUBSTR(vendor_city, '^SAN|LOS') IS NOT NULL;
```

### REGEXP_REPLACE and REGEXP_LIKE functions

```sql
SELECT vendor_name, vendor_address1,
   REGEXP_REPLACE(vendor_address1, 'STREET', 'St') AS new_address1
FROM Vendors
WHERE REGEXP_LIKE(vendor_address1, 'STREET');
```

## Ranking functions

These are non-aggregate window functions, sometimes called specialiazed window functions. These functions are grouped into 2 groups: Ranking functions and analytical functions.

### ROW_NUMBER function

```sql
SELECT ROW_NUMBER() OVER(PARTITION BY vendor_state                  (2), (3)
   ORDER BY vendor_name) AS 'row_number', vendor_name, vendor_state (1)
FROM vendors;
```
1. Detemines the sequence of the rows within the partitions
2. Specifies the column that's used to divide the result set into groups.
3. Returns the number of the current row within its partition, starting at 1 for the first row in each partition.

### RANK and DENSE_RANK functions

Both functions return the rank of each row within the partition of a result set. If there is a tie, both of these functions give the same rank to all rows that are tied. 

```sql
SELECT RANK() OVER(ORDER BY invoice_total) AS 'rank',           (1)
   DENSE_RANK() OVER (ORDER BY invoice_total) AS 'dense_rank',  (2)
   invoice_total, invoice_number
FROM invoices;
```
1. To determine the rank for the next distinct row, **RANK** adds 1 to the total number of rows.
2. To determine the rank for the next distinct row, **DENSE_RANK** adds 1 to the rank for the previous row.

### NTILE function

This function divides the rows in a partition into a specified number of groups and returns the group number of each row.

```sql
SELECT terms_description,
   NTILE(2) OVER (ORDER BY terms_id) AS tile2,
   NTILE(3) OVER (ORDER BY terms_id) AS tile3,
   NTILE(4) OVER (ORDER BY terms_id) AS tile4,
FROM terms;
```

## Analytic functions

These functions let you perform calculations on ordered sets of data.  

The **FIRST_VALUE**, **LAST_VALUE**, and **NTH_VALUE** let you return the first, last, and nth values in an ordered set of values. When you use the **PARTITION BY** clause with **LAST_VALUE** or **NTH_VALUE**, you typically include the **ROWS** or **RANGE** clause as well to define a subset of the current partition.

### FIRST_VALUE, NTH_VALUE, and LAST_VALUE functions
```sql
SELECT sales_year, CONCAT(rep_first_name, ' ', rep_last_name) AS rep_name, sales total,
   FIRST_VALUE(CONCAT(rep_first_name, ' ', rep_last_name))
       OVER (PARTITION BY sales_year ORDER BY sales_total DESC)
       AS highest_sales,
    NTH_VALUE(CONCAT(rep_first_name, ' ', rep_last_name), 2)
       OVER (PARTITION BY sales_year ORDER BY sales_total DESC
       RANGE BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING)
       AS second_highest_sales,
    LAST_VALUE(CONCAT(rep_first_name, ' ', rep_last_name))
       OVER(PARTITION BY sales_year ORDER BY sales_total DESC
       RANGE BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING)
       AS lowest_sales
FROM sales_totals JOIN sales_reps ON sales_totals.rep_id = sales_reps.rep_id;
```

### LAG function

```sql
SELECT rep_id, sales_year, sales_total AS current_sales,
   LAG(sales_total, 1, 0) OVER (PARTITION BY rep_id ORDER BY sales_year)    (1), (2)
      AS last_sales,
   sales_total - LAG(sales_total, 1, 0)
      OVER (PARTITION BY rep_id ORDER BY sales_year) AS 'change'            (1)
FROM sales_totals;
```
1. **OVER** clause is used to group the result set by the rep_id column and sort it by the sales_year column.
2. **LAG** function gets the sales total from one row prior to the current row (the offset).

### PERCENT_RANK and CUME_DIST functions

The **PERCENT_RANK** calculates the rank of the values in a sorted set of values as a percent. Calculates a percent that indicates the rank of each row within a partition. The result of this function is always 0 or 1.  

The **CUME_DIST** function calculates the percent of the values in a sorted set of values that are less than or equal to the current value. This represents the cumulative distribution - calculated by dividing the number of rows with the current value or a lower value by the total nubmer of rows in the partition.

```sql
SELECT sales_year, rep_id, sales_total,
   PERCENT_RANK() OVER (PARTITION BY sales_year ORDER BY sales_total)
      AS pct_rank,
   CUME_DIST() OVER (PARTITION BY sales_year ORDER BY sales_total)
      AS 'cume_dist'
FROM sales_totals;
```

# Working with databases

## Creating a database
```sql
CREATE DATABASE [IF NOT EXISTS] dbName
```

## Dropping a database
```sql
CREATE DATABASE [IF EXISTS] dbName
```

## Use statement

The **USE** statement selects the specified database and makes it the current database.

## Creating a table

The **CREATE TABLE** statement creates a new table in the current database. Alternately, you can qualify the table name with the correct database. For example, ```sql CREATE TABLE dbName.tableName;```.

### Common column attributes

| Attribute     | Description       |
|:--------------|:------------------|
| NOT NULL      | Indicates that the column doesn't accept null values. If omitted, the column can accept null values. |
| UNIQUE        | Specifies that each value stored in the column must be unique. |
| DEFAULT default_value | Specifies a defalut value for the column as a literal or as an expression    |
| AUTO_INCREMENT    | Identifies a column whose value is incremented automatically when a new row is added. An auto increment column must be defined as an integer or floating-point number. |

**NOTE**: NULL and UNIQUE are types of constraints.

### Create a table without column attributes
```sql
CREATE TABLE vendors
(
    vendor_id       INT,
    vendor_name     VARCHAR(50)
)
```

### Create a table with column attributes
```sql
CREATE TABLE vendors
(
    vendor_id       INT             NOT NULL        UNIQUE AUTO_INCREMENT,
    vendor_name     VARCHAR(50)     NOT NULL        UNIQUE  
)
```

## Coding a primary key constraint

Constraints are used to enforce the integrity of the data in a table by defining rules about the values that can be stored in the columns of the table.

When you identify a column as the primary key, the following happens:
- the column is forced to be **NOT NULL**
- the column is forced to contain a unique value for each row.
- An index is created automatically based on the column.

### Column-level constraints

Code a column-level constraint as part of the definition of the column it constrains.

```sql
CREATE TABLE vendors
(
    vendor_id       INT             PRIMARY KEY         AUTO_INCREMENT,
    vendor_name     VARCHAR(50)     NOT NULL            UNIQUE
)
```

### Table-level constraints

Code a table-level constraint as if it is a separate column definition, and you name the columns it constrains within that definition.

```sql
CREATE TABLE vendors
(
    vendor_id           INT             AUTO_INCREMENT,
    vendor_name         VARCHAR(50)     NOT NULL,
    CONSTRAINT vendors_pk PRIMARY KEY (vendor_id),
    CONSTRAINT vendor_name_uq UNIQUE (vendor_name)
)
```

## Foreign-key constraints

Also known as a _reference constraint_. This constraint requires values in one tabvle to match values in another table. Used to define the relationship between tables and to enforce referential integrity.   

### Column-level foreign key constraint

To create a foreign key constraing at the column level, you code the **REFERENCES** keyword followed by the name of the related table and the name of the related colum nin parentheses.

```sql
CREATE TABLE invoices
(
    invoice_id          INT             PRIMARY KEY,
    vendor_id           INT             REFERENCES vendors (vendor_id),
    invoice_number      VARCHAR(50)     NOT NULL        UNIQUE
)
```

### Table-level foreign key constraint

To create a foreign key constraing at the table level, include the **CONSTRAINT** keyword followed by a name, followed by the **FOREIGN KEY** keywords. This allows you to provide a name for the foreign key, which is a best practice.

```sql
CREATE TABLE invoices
(
    invoice_id          INT             PRIMARY KEY,
    vendor_id           INT             NOT NULL,
    invoice_number      VARCHAR(50)     NOT NULL        UNIQUE,
    CONSTRAINT invoices_fk_vendors
       FOREIGN KEY (vendor_id) REFERENCES vendors (vendor_id)
)
```

## Alter constraints of a table

Use the **ALTER TABLE** statement to add or drop the constraints of an existing table

### Adds a new column

```sql
ALTER TABLE vendors
ADD last_transaction_date DATE
```

### Drops a column

```sql
ALTER TABLE vendors
DROP COLUMN last_transaction_date
```

### Change the length of the column

```sql
ALTER TABLE vendors
MODIFY vendor_name VARCHAR(100) NOT NULL
```

### Change data type

```sql
ALTER TABLE vendors
MODIFY vendor_name CHAR(100) NOT NULL
```

### Change default value of a column

```sql
ALTER TABLE vendors
MODIFY vendor_name VARCHAR(100) NOT NULL DEFAULT 'New Vendor';
```

## Change name

```sql
ALTER TABLE vendors
RENAME COLUMN vendor_name TO v_name;
```

## Alter the constraints of a table

To drop a foreign key constraint, yoiu must know its name. If you don't, use a GUI tool to look it up.

### Add a primary key constraint

```sql
ALTER TABLE vendors
ADD PRIMARY KEY (vendor_id)
```

### Add a foreign key constraint

```sql
ALTER TABLE invoices
ADD CONSTRAINT invoice_fk_vendors
   FOREIGN KEY (vendor_id) REFERENCES vendors (vendor_id)
```

### Drop primary key constraint

```sql
ALTER TABLE vendors
DROP PRIMARY KEY
```

### Drop foreign key constraint

```sql
ALTER TABLE invoices
DROP PRIMARY KEY invoice_fk_vendors
```

## Rename, truncate, and drop a table

Be careful with these statements!

### Rename a table

```sql
RENAME TABLE vendors TO vendor
```

### Delete all data from a table 

```sql
TRUNCATE TABLE vendor
```

### Delete table from the current database

```sql
DROP TABLE vendor
```

### Qualifies the table to be deleted

```sql
DROP TABLE ex.vendor
```

## Indexes

An index speeds up joins and searches by providing a way for a database management system to go directly to a row rather than having to search through all the rows until if finds the one that you want. By default, MySQL creates indexes for primary keys, foreign keys, and uique keys of a table.  

You may want to create indexes for other columns that are used frequently in search conditions or joins. Avoid creating indexes on columns that are updated frequently since this slows down insert, update, and delete operations. You can also drop indexes from a table.

### Standard index naming convention

```sql
table_column_ix
```

```sql
invoices_invoice_date_ix
```

### Create index based on single column

```sql
CREATE INDEX invoices_invoice_date_ix
   ON invoices (invoice_date)
```

### Creates an index based on two columns

```sql
CREATE INDEX invoices_vendor_id_invoice_number_ix
   ON invoices (invoice_id, invoice_number)
```

### Creates a unique index

```sql
CREATE UNIQUE INDEX vendors_vendor_phone_ix
   ON vendors (vendor_phone)
```

### Creates an index sorted in DESC 

```sql
CREATE INDEX invoices_invoice_total_ix
   ON invoices (vendor_phone DESC)
```

### Drops an index

```sql
DROP INDEX vendors_vendor_phone_ix ON vendors
```

## A script that creates an entire database

A script is a file that contains one or more SQL statements. You must create the tables that don't have foreign keys ffirst. That way, the other tables can define foreign keys that refer to them.

```sql
-- create the database
DROP DATABASE IF EXISTS ap;
CREATE DATABASE ap;

-- select the database
USE ap;

-- create the tables
CREATE TABLE general_ledger_accounts
(
  account_number        INT            PRIMARY KEY,
  account_description   VARCHAR(50)    UNIQUE
);

CREATE TABLE terms
(
  terms_id              INT            PRIMARY KEY,
  terms_description     VARCHAR(50)    NOT NULL,
  terms_due_days        INT            NOT NULL
);

CREATE TABLE vendors
(
  vendor_id                     INT            PRIMARY KEY   AUTO_INCREMENT,
  vendor_name                   VARCHAR(50)    NOT NULL      UNIQUE,
  vendor_address1               VARCHAR(50),
  vendor_address2               VARCHAR(50),
  vendor_city                   VARCHAR(50)    NOT NULL,
  vendor_state                  CHAR(2)        NOT NULL,
  vendor_zip_code               VARCHAR(20)    NOT NULL,
  vendor_phone                  VARCHAR(50),
  vendor_contact_last_name      VARCHAR(50),
  vendor_contact_first_name     VARCHAR(50),
  default_terms_id              INT            NOT NULL,
  default_account_number        INT            NOT NULL,
  CONSTRAINT vendors_fk_terms
    FOREIGN KEY (default_terms_id)
    REFERENCES terms (terms_id),
  CONSTRAINT vendors_fk_accounts
    FOREIGN KEY (default_account_number)
    REFERENCES general_ledger_accounts (account_number)
);
CREATE TABLE invoices
(
  invoice_id            INT            PRIMARY KEY   AUTO_INCREMENT,
  vendor_id             INT            NOT NULL,
  invoice_number        VARCHAR(50)    NOT NULL,
  invoice_date          DATE           NOT NULL,
  invoice_total         DECIMAL(9,2)   NOT NULL,
  payment_total         DECIMAL(9,2)   NOT NULL      DEFAULT 0,
  credit_total          DECIMAL(9,2)   NOT NULL      DEFAULT 0,
  terms_id              INT            NOT NULL,
  invoice_due_date      DATE           NOT NULL,
  payment_date          DATE,
  CONSTRAINT invoices_fk_vendors
    FOREIGN KEY (vendor_id)
    REFERENCES vendors (vendor_id),
  CONSTRAINT invoices_fk_terms
    FOREIGN KEY (terms_id)
    REFERENCES terms (terms_id)
);

CREATE TABLE invoice_line_items
(
  invoice_id              INT            NOT NULL,
  invoice_sequence        INT            NOT NULL,
  account_number          INT            NOT NULL,
  line_item_amount        DECIMAL(9,2)   NOT NULL,
  line_item_description   VARCHAR(100)   NOT NULL,
  CONSTRAINT line_items_pk
    PRIMARY KEY (invoice_id, invoice_sequence),
  CONSTRAINT line_items_fk_invoices
    FOREIGN KEY (invoice_id)
    REFERENCES invoices (invoice_id),
  CONSTRAINT line_items_fk_acounts
    FOREIGN KEY (account_number)
    REFERENCES general_ledger_accounts (account_number)
);

-- create an index
CREATE INDEX invoices_invoice_date_ix
  ON invoices (invoice_date DESC);
```

# Storage engines

A storage engine determines how MySQL stores data and which database features are available to you.

## View all the storage engines available on the server

```sql
SHOW ENGINES;
```

## View the default storage engine for a server

```sql
SHOW VARIABLES LIKE 'default_storage_engine';
```

## View the storage engine for all the tables in a database

```sql
SELECT table_name, engine
FROM information_schema.tables
WHERE table_schema = 'ap';
```

## Specify a storage engine for a table
```sql
CREATE TABLE product_descriptions
(
    product_id              INT             PRIMARY KEY,
    product_description     VARCHAR(200)    
)
ENGINE = MyISAM;
```
## Specify an engine for an existing table
```sql
ALTER TABLE product_descriptions ENGINE = InnoDB;
```

## Set the default storage engine for the current session

```sql
SET SESSION default_storage_engine = InnoDB;
```

# Create views

A view is a **SELECT** statement that is stored in the database as a database object. Think of it as a virtyal table that consists of only the rows and columns specified in its **CREATE VIEW** statement.

When you save queries, you can store them in a script or you can save them in a view. Views are not stored in files, they are stored as part of the database. So, they can be used by SQL programmers and by custom applications that have access to the database.

## Create view statement for view named vendors_min

```sql
CREATE VIEW vendors_min AS 
   SELECT vendor_name, vendor_state, vendor_phone
   FROM vendors;
```

```sql
CREATE VIEW vendors_sw AS
SELECT *
FROM vendors
WHERE vendor_state IN ('CA', 'AZ', 'NV', 'NM');
```

## SELECT statement that uses vendors_min view

```sql
SELECT * FROM vendors_min
WHERE vendor_state = 'CA'
ORDER BY vendor_name;
```

## UPDATE statement that uses vendors_min view

```sql
UPDATE vendors_min
SET vendor_phone = '(800) 555-3941'
WHERE vendor_name = 'Register of Copyrights';
```

## Drop a view

```sql
DROP VIEW vendors_min;
```

## Using REPLACE

When you code a view, you can specify that you want to automatically drop a view that has the same name as the view that you're creating by using the **OR REPLACE** keywords after the **CREATE** keyword.

```sql
CREATE OR REPLACE VIEW vendor_invoices AS 
   SELECT vendor_name, invoice_number, invioce_date, invoice_total
   FROM vendors
      JOIN invoices ON vendors.vendor_id = invoices.vendor_id;
```

## Updatable view

To be an updatable view, a view must meet the following requirements:
- The **SELECT** list can't include the **DISTINCT** keyword or an aggregate function
- The **SELECT** statement can't include a **GROUP BY** or **HAVING** clause
- Two **SELECT** statements cannot be joined by a union operation

To **INSERT** rows into views, you must make sure that the **INSERT** statement includes the all the rows as the view. 

If a view is updatable, you can use the **INSERT**, **UPDATE**, or **DELETE** clauses with them. If a view isn't updatable, its a read-only view.

## WITH CHECK option clause

If you specify a **WITH CHECK OPTION** clause when you creat a view, an error will occur if you try to modify a row in such a way that it would no longer be included in the view.  
This clause prevents an update if it causes the row to be excluded from the view.

```sql
CREATE OR REPLACE VIEW vendor_payment AS
   SELECT vendor_name, invoice_number, invoice_date, payment_date,
      invoice_total, credit_total, payment_total
   FROM vendors JOIN invoices ON vendors.vendor_id = invoices.vendor_id
   WHERE invoice_total - payment_total - credit_total >= 0
WITH CHECK OPTION;
```

# Stored programs

Stored programs include procedural code that controls the flow of programs.

| Type       | Description       |
|:-----------|:------------------|
| Stored procedure  | Can be called from an application that has access to the database. |
| Stored function   | Can be called from a SQL statement. A stored function works much like the native functions like **CONCAT**. |
| Trigger           | Is executed in response to an **INSERT**, **UPDATE**, or **DELETE** statement on a specified table. |
| Event             | Is executed at a scheduled time.  |

## Script for stored procedure named test

**NOTE**: The **DELIMITER //** statement changes the delimter from the default semicolon delimiter (;) to two slashed (//)

```sql
USE ap;

DROP PROCEDURE IF EXISTS test;

-- Change statement delimiter from semicolon to double front slash 
DELIMITER //

CREATE PROCEDURE test()
BEGIN 
   DECLARE sum_balance_due_var DECIMAL(9, 2);

   SELECT SUM(invoice_total - payment_total - credit_total)
   INTO sum_balance_due_var
   FROM invoices
   WHERE vendor_id = 95;

   IF sum_balance_due_var > 0 THEN
      SELECT CONCAT('Balance due: $', sum_balance_due_var) AS message;
    ELSE
       SELECT 'Balance paid in full' AS message;
   END IF;
END//

-- Change statement delimiter from double front slash to semicolon 
DELIMITER ;

CALL test();
```

### Flow of execution keywords

| Keywords  | Description     |
|:----------|:----------------|
| IF...ELSEIF...ELSE | Controls the flow of execution based on a condition |
| CASE...WHEN...ELSE | Controls the flow of execution based ona  condition |
| WHILE...DO...LOOP | Repeats statements while a condition is true |
| REPEAT...UNTIL...END REPEAT | Repeats statements while a condition is true |
| DECLARE...CURSOR FOR | Defines a result set that can be processed by a loop. |
| DECLARE...HANDLER | Defines a handler that's executed when a stroed program encounters and error. |

### Display data and debug

```sql
DELIMITER //

CREATE PROCEDURE test()
BEGIN
   SELECT 'This is a test.' AS messages;
END//
```

### How to declare and set variables

The following sets a variable to a literal value or an expression:
```sql
SET variable_name = {literal_value|expression};
SET vendor_id_var = 95;
```

The following sets a variable to a selected value
```sql
SELECT column_1[, column_2]...
INTO variable_name_1[, variable_name_2]...

SELECT MAX(invoice_total), MIN(invoice_total), COUNT(invoice_id)
INTO max_invoice_total, min_invoice_total, count_invoice_id
```

```sql
USE ap;

DROP PROCEDURE IF EXISTS test;

DELIMITER //

CREATE PROCEDURE test()
BEGIN
  DECLARE max_invoice_total  DECIMAL(9,2);
  DECLARE min_invoice_total  DECIMAL(9,2);
  DECLARE percent_difference DECIMAL(9,4);
  DECLARE count_invoice_id   INT;
  DECLARE vendor_id_var      INT;
  
  SET vendor_id_var = 95;

  SELECT MAX(invoice_total), MIN(invoice_total), COUNT(invoice_id)
  INTO max_invoice_total, min_invoice_total, count_invoice_id
  FROM invoices WHERE vendor_id = vendor_id_var;

  SET percent_difference = (max_invoice_total - min_invoice_total) / 
                         min_invoice_total * 100;
  
  SELECT CONCAT('$', max_invoice_total) AS 'Maximum invoice', 
         CONCAT('$', min_invoice_total) AS 'Minimum invoice', 
         CONCAT('%', ROUND(percent_difference, 2)) AS 'Percent difference',
         count_invoice_id AS 'Number of invoices';
END//

DELIMITER ;

CALL test();
```

### Stored procedure that uses an IF statement
```sql
USE ap;

DROP PROCEDURE IF EXISTS test;

DELIMITER //

CREATE PROCEDURE test()
BEGIN
   DECLARE first_invoice_due_date DATE;

   SELECT MIN(invoice_due_date)
   INTO first_invoice_due_date
   FROM invoices
   WHERE invoice_total - payment_total - credit_total > 0;

   IF first_invoice_due_date < NOW() THEN
     SELECT 'Outstanding invoices are overdue!';
   ELSEIF first_invoice_due_date = SYSDATE() THEN
     SELECT 'Outstanding invoices are due today!';
   ELSE
     SELECT 'No invoices are overdue.';
   END IF;

  -- the IF statement rewritten as a Searched CASE statement
  /*
  CASE  
    WHEN first_invoice_due_date < NOW() THEN
      SELECT 'Outstanding invoices overdue!' AS Message;
    WHEN first_invoice_due_date = NOW() THEN
      SELECT 'Outstanding invoices are due today!' AS Message;
    ELSE
      SELECT 'No invoices are overdue.' AS Message;
  END CASE;
  */
  
END//

DELIMITER ;

CALL test();
```

### Case statements

Similar to a switch statement in Java.

```sql
USE ap;

DROP PROCEDURE IF EXISTS test;

DELIMITER //

CREATE PROCEDURE test()
BEGIN
  DECLARE terms_id_var INT;

  SELECT terms_id INTO terms_id_var 
  FROM invoices WHERE invoice_id = 4;

  CASE terms_id_var
    WHEN 1 THEN 
      SELECT 'Net due 10 days' AS Terms;
    WHEN 2 THEN 
      SELECT 'Net due 20 days' AS Terms;      
    WHEN 3 THEN 
      SELECT 'Net due 30 days' AS Terms;      
    ELSE
      SELECT 'Net due more than 30 days' AS Terms;
  END CASE;
```