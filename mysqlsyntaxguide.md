                    <!-- MySQL syntax guide -->



        <!-- How to login into mysql from terminal -->

To log in via SSH as the root user: enter the MySQL command line with this command:
sudo mysql -u root -p
or
mysql -u USERNAME -pPASSWORD -h HOSTNAME mydb

                <!-- How to SHOW USERS -->

Unlike the SHOW DATABASES or SHOW TABLES commands that display all databases or tables right away, the SHOW USERS command does not exist in MySQL. Users can use a MySQL query and get a full list of users in a given MySQL database server: 

SELECT user FROM mysql.user;


                <!-- How to CREATE USERS -->

The CREATE USER statement creates new MySQL accounts and enables authentication, role, SSL/TLS, resource-limit, password-management, comment, and attribute properties to be established for new accounts. To use CREATE USER, you must have the global CREATE USER privilege, or the INSERT privilege for the mysql system schema.

mysql> CREATE USER 'local_user'@'localhost' IDENTIFIED BY 'password';


                <!-- How to GRANT PRIVILEGES, Show granted privileges and remove -->

GRANT: assign new privileges to a user account
REVOKE: remove existing privileges from a user account
GRANT OPTION: the GRANT OPTION privilege allows you to grant or revoke any privilege that you have been granted

To grant a privilege with GRANT, you must have the GRANT OPTION privilege, and you must have the privileges that you are granting. (Alternatively, if you have the UPDATE privilege for the grant tables in the mysql system schema, you can grant any account any privilege.) 

SHOW GRANTS; <!-- view the privileges granted to your own user -->

SHOW GRANTS FOR '<user>'@'<host>'; <!--If the user account you are logged in as has SELECT privileges on the internal mysql database, you can see the privileges granted to other user accounts. To show the privileges of other accounts-->

GRANT ALL ON <!--databasename-->.* TO 'user'@'localhost';

GRANT 'role1', 'role2' TO 'user1'@'localhost', 'user2'@'localhost';

GRANT SELECT ON <!--databasename-->.* TO 'role3';

<!-- Account name syntax is 'user_name'@'host_name'.

The @'host_name' part is optional. An account name consisting only of a user name is equivalent to 'user_name'@'%'. For example, 'me' is equivalent to 'me'@'%'.

The user name and host name need not be quoted if they are legal as unquoted identifiers.  -->


GRANT ALL PRIVILEGES ON sales.* TO 'salesadmin'@'localhost'; <!-- assign full privileges to a user at a specific scope using the ALL or ALL PRIVILEGES -->



            <!-- How to SHOW, DELETE & CREATE DATABASES & SELECT DATABASES -->

mysql> SHOW DATABASES; <!--Show-->
mysql> CREATE DATABASE <!--databasename--> ; <!--Create-->
mysql> DROP DATABASE <!--databasename-->; <!--Delete-->
USE DatabaseName; <!--Select-->

        <!-- How to CREATE a TABLE with Columns and their data types -->

In MySQL there are three main data types: string, numeric, and date and time.

CREATE TABLE table_name(
   column1 datatype,
   column2 datatype,
   column3 datatype,
   .....
   columnN datatype,
   PRIMARY KEY( one or more columns )
);

CREATE TABLE new_table_name AS
    SELECT column1, column2,...
    FROM existing_table_name
    WHERE ....; <!--create a new table using an existing table, the new table will be filled with the existing values from the old table.-->

<!-- String Data Types: -->

CHAR(size)	A FIXED length string (can contain letters, numbers, and special characters). The size parameter specifies the column length in characters - can be from 0 to 255. Default is 1

VARCHAR(size)	A VARIABLE length string (can contain letters, numbers, and special characters). The size parameter specifies the maximum column length in characters - can be from 0 to 65535

BINARY(size)	Equal to CHAR(), but stores binary byte strings. The size parameter specifies the column length in bytes. Default is 1

VARBINARY(size)	Equal to VARCHAR(), but stores binary byte strings. The size parameter specifies the maximum column length in bytes.

TINYBLOB	For BLOBs (Binary Large OBjects). Max length: 255 bytes

TINYTEXT	Holds a string with a maximum length of 255 characters

TEXT(size)	Holds a string with a maximum length of 65,535 bytes

BLOB(size)	For BLOBs (Binary Large OBjects). Holds up to 65,535 bytes of data

MEDIUMTEXT	Holds a string with a maximum length of 16,777,215 characters

MEDIUMBLOB	For BLOBs (Binary Large OBjects). Holds up to 16,777,215 bytes of data

LONGTEXT	Holds a string with a maximum length of 4,294,967,295 characters

LONGBLOB	For BLOBs (Binary Large OBjects). Holds up to 4,294,967,295 bytes of data

ENUM(val1, val2, val3, ...)	A string object that can have only one value, chosen from a list of possible values. You can list up to 65535 values in an ENUM list. If a value is inserted that is not in the list, a blank value will be inserted. The values are sorted in the order you enter them

SET(val1, val2, val3, ...)	A string object that can have 0 or more values, chosen from a list of possible values. You can list up to 64 values in a SET list


<!-- Numeric Data Types -->

<!-- All the numeric data types may have an extra option: UNSIGNED or ZEROFILL. If you add the UNSIGNED option, MySQL disallows negative values for the column. If you add the ZEROFILL option, MySQL automatically also adds the UNSIGNED attribute to the column. -->


BIT(size)	A bit-value type. The number of bits per value is specified in size. The size parameter can hold a value from 1 to 64. The default value for size is 1.

TINYINT(size)	A very small integer. Signed range is from -128 to 127. Unsigned range is from 0 to 255. The size parameter specifies the maximum display width (which is 255)

BOOL	Zero is considered as false, nonzero values are considered as true.

BOOLEAN	Equal to BOOL

SMALLINT(size)	A small integer. Signed range is from -32768 to 32767. Unsigned range is from 0 to 65535. The size parameter specifies the maximum display width (which is 255)

MEDIUMINT(size)	A medium integer. Signed range is from -8388608 to 8388607. Unsigned range is from 0 to 16777215. The size parameter specifies the maximum display width (which is 255)

INT(size)	A medium integer. Signed range is from -2147483648 to 2147483647. Unsigned range is from 0 to 4294967295. The size parameter specifies the maximum display width (which is 255)

INTEGER(size)	Equal to INT(size)

BIGINT(size)	A large integer. Signed range is from -9223372036854775808 to 9223372036854775807. Unsigned range is from 0 to 18446744073709551615. The size parameter specifies the maximum display width (which is 255)

FLOAT(size, d)	A floating point number. The total number of digits is specified in size. The number of digits after the decimal point is specified in the d parameter. This syntax is deprecated in MySQL 8.0.17, and it will be removed in future MySQL versions

FLOAT(p)	A floating point number. MySQL uses the p value to determine whether to use FLOAT or DOUBLE for the resulting data type. If p is from 0 to 24, the data type becomes FLOAT(). If p is from 25 to 53, the data type becomes DOUBLE()

DOUBLE(size, d)	A normal-size floating point number. The total number of digits is specified in size. The number of digits after the decimal point is specified in the d parameter

DOUBLE PRECISION(size, d)	 

DECIMAL(size, d)	An exact fixed-point number. The total number of digits is specified in size. The number of digits after the decimal point is specified in the d parameter. The maximum number for size is 65. The maximum number for d is 30. The default value for size is 10. The default value for d is 0.

DEC(size, d)	Equal to DECIMAL(size,d)

<!-- Date and Time Data Types -->


DATE	A date. Format: YYYY-MM-DD. The supported range is from '1000-01-01' to '9999-12-31'

DATETIME(fsp)	A date and time combination. Format: YYYY-MM-DD hh:mm:ss. The supported range is from '1000-01-01 00:00:00' to '9999-12-31 23:59:59'. Adding DEFAULT and ON UPDATE in the column definition to get automatic initialization and updating to the current date and time

TIMESTAMP(fsp)	A timestamp. TIMESTAMP values are stored as the number of seconds since the Unix epoch ('1970-01-01 00:00:00' UTC). Format: YYYY-MM-DD hh:mm:ss. The supported range is from '1970-01-01 00:00:01' UTC to '2038-01-09 03:14:07' UTC. Automatic initialization and updating to the current date and time can be specified using DEFAULT CURRENT_TIMESTAMP and ON UPDATE CURRENT_TIMESTAMP in the column definition

TIME(fsp)	A time. Format: hh:mm:ss. The supported range is from '-838:59:59' to '838:59:59'

YEAR	A year in four-digit format. Values allowed in four-digit format: 1901 to 2155, and 0000.

<!-- MySQL 8.0 does not support year in two-digit format. -->


        <!-- How to SHOW, DELETE & DROP Tables -->

SHOW TABLES; <!--to see all tables in a database-->
SHOW TABLES LIKE 'a%'; <!--you will only see a filtered list of tables -->

DROP TABLE table_name; <!--used to drop an existing table in a database.-->

TRUNCATE TABLE table_name; <!--TRUNCATE TABLE statement is used to delete the data inside a table, but not the table itself-->


        <!-- How to Insert ROWS & RECORDS (single and multiple) -->
<!-- The INSERT INTO statement is used to insert new records in a table. -->

INSERT INTO table_name (column1, column2, column3, ...)
VALUES (value1, value2, value3, ...);

<!-- If you are adding values for all the columns of the table, you do not need to specify the column names in the SQL query. -->

INSERT INTO table_name
VALUES (value1, value2, value3, ...);

        <!-- How to SELECT with the WHERE Clause -->

<!-- The WHERE clause is used to filter records and is used to extract only those records that fulfill a specified condition. It is not only used in SELECT statements, it is also used in UPDATE, DELETE, etc.! -->

SELECT column1, column2, ...
FROM table_name
WHERE condition;

        <!-- How to SELECT with the WHERE Clause using a range -->

SELECT 
    column_1, column_2
FROM
    table
WHERE
    (expr | column) BETWEEN lower_value AND upper_value;

<!-- The BETWEEN operator is used in the WHERE clause to select a value within a range of values. We often use the BETWEEN operator in the WHERE clause of the SELECT, UPDATE and DELETE statements. -->

          <!-- How to DELETE an individual ROW -->

DELETE FROM table_name WHERE condition; <!--The DELETE statement is used to delete existing records in a table.-->

          <!-- How to UPDATE a ROW -->

          UPDATE table_name
SET column1 = value1, column2 = value2, ...
WHERE condition;

<!-- The UPDATE statement is used to modify the existing records in a table. -->

         UPDATE Multiple Records

UPDATE Table
SET Column = value;

<!-- If you omit the WHERE clause, ALL records will be updated! -->
          <!-- How to add a new column and modify it -->

<!-- The ALTER TABLE statement is used to add, delete, or modify columns in an existing table.

The ALTER TABLE statement is also used to add and drop various constraints on an existing table. -->

ALTER TABLE table_name
ADD column_name datatype;

ALTER TABLE table_name
DROP COLUMN column_name; <!--To delete a column in a table-->

ALTER TABLE table_name
RENAME COLUMN old_name to new_name; <!--To rename a column in a table-->

ALTER TABLE table_name
ALTER COLUMN column_name datatype; <!--To change the data type of a column in a table-->

MODIFY COLUMN column_name datatype; <!--My SQL / Oracle (prior version 10G):-->
MODIFY column_name datatype;<!--Oracle 10G and later:-->

          <!-- How to Order by and use Distinct -->

<!-- the ORDER BY clause to sort the result set of a MySQL query, and the DISTINCT keyword to eliminate duplicate rows from the result set -->

SELECT DISTINCT column1, column2, ...
FROM your_table
ORDER BY column_to_sort (DESC to sort in descending order, );

<!-- The DISTINCT keyword ensures that only unique combinations of the selected columns are included in the result set. -->

          <!-- How to Concatenate Columns -->

<!-- you can concatenate columns using the CONCAT() function. The CONCAT() function is used to concatenate two or more strings or columns into a single string. -->

SELECT CONCAT(column1, ' ', column2) AS concatenated_columns
FROM your_table;

SELECT CONCAT_WS(', ', column2, column1) AS concatenated_columns
FROM your_table; <!-- use the CONCAT_WS() function if you want to concatenate with a specified separator-->


          <!-- How to Select Distinct Rows -->

SELECT DISTINCT
    select_list
FROM
    table_name
WHERE 
    search_condition
ORDER BY 
    sort_expression;

<!--In this syntax, you specify one or more columns that you want to select distinct values after the SELECT DISTINCT keywords.

If you specify one column, the DISTINCT clause will evaluate the uniqueness of rows based on the values of that column.

However, if you specify two or more columns, the DISTINCT clause will use the values of these columns to evaluate the uniqueness of the rows.

When executing the SELECT statement with the DISTINCT clause, MySQL evaluates the DISTINCT clause after the FROM, WHERE, and SELECT clause and before the ORDER BY clause: -->


          <!-- How to use LIKE to Search -->

SELECT column1, column2, ...
FROM your_table
WHERE column_to_search LIKE 'pattern'; 

<!-- the LIKE operator is used to search for a specified pattern in a column. The LIKE operator can be used with wildcard characters to make the search more flexible -->

the wildcard characters commonly used with the LIKE operator:

%: Represents zero or more characters.
_: Represents a single character.


          <!-- How Select using IN -->

SELECT column1, column2, ...
FROM your_table
WHERE column_to_check IN (value1, value2, ...);

<!-- The IN operator in MySQL is used to specify a range of values in a WHERE clause. It allows you to filter rows based on a set of specified values. -->


          <!-- How to Create & Remove Index -->

CREATE INDEX index_name
ON table_name (column1, column2, ...);

 <!-- you can create and remove indexes using the CREATE INDEX and DROP INDEX statements. Indexes are used to speed up the retrieval of rows from a table by creating a data structure that provides faster access to the rows based on the values in one or more columns. -->

 DROP INDEX index_name
ON table_name;

 <!-- To remove an index, you can use the DROP INDEX statement. -->