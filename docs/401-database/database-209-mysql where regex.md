---
layout: default
title: database mysql where regex
parent: database
nav_order: 401209
---

```sql
SELECT telephone_number
FROM table
WHERE telephone_number REGEXP '^1[() -]*[[:digit:]]{3}[() -]*[[:digit:]]{3}[() -]*[[:digit:]]{4}$';
```
