---
layout: page
title: Code & Query
permalink: code
---

### SQL is for ballers.  
Are you a baller? Then this should appeal.

```sql
SELECT column1, column2 
FROM table t
WHERE column1='value';
```

This query got me back some hella sweet data:

| column1 | column2 |
|---------|---------|
| foo | bar |
| foo | bar |
| foo | bar |


### Here's some rad python, with super-dope colors

```python
# Program to display the Fibonacci sequence up to n-th term

nterms = int(input("How many terms? "))

# first two terms
n1, n2 = 0, 1
count = 0

# check if the number of terms is valid
if nterms <= 0:
   print("Please enter a positive integer")
# if there is only one term, return n1
elif nterms == 1:
   print("Fibonacci sequence upto",nterms,":")
   print(n1)
# generate fibonacci sequence
else:
   print("Fibonacci sequence:")
   while count < nterms:
       print(n1)
       nth = n1 + n2
       # update values
       n1 = n2
       n2 = nth
       count += 1
```

