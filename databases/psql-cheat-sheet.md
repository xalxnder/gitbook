# PSQL Cheat Sheet

| **Command**                                                   | **Description**                          |
| ------------------------------------------------------------- | ---------------------------------------- |
| psql -U username -d database                                  | Connect to a PostgreSQL database.        |
| \c database\_name                                             | Switch to another database.              |
| \l                                                            | List all databases.                      |
| \dt                                                           | List all tables in the current database. |
| \d table\_name                                                | Show schema/details of a table.          |
| SELECT \* FROM table\_name;                                   | Retrieve all rows from a table.          |
| INSERT INTO table\_name (col1, col2) VALUES ('val1', 'val2'); | Insert data into a table.                |
| UPDATE table\_name SET column='value' WHERE condition;        | Update data in a table.                  |
| DELETE FROM table\_name WHERE condition;                      | Delete data from a table.                |
| CREATE TABLE table\_name (col1 TYPE, col2 TYPE);              | Create a new table.                      |
| DROP TABLE table\_name;                                       | Delete a table.                          |
| \q                                                            | Exit psql.                               |
| ?                                                             | Show help for psql commands.             |
| \h                                                            | Show help for SQL commands.              |
| \x                                                            | Toggle extended display mode.            |
