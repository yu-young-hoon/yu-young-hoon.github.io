---
layout: default
title: database mysql order by numbering
parent: database
nav_order: 401206
---

```sql
SELECT 
    @rownum:=@rownum + 1 AS RNUM
    , a.*
FROM
    some_table AS a,
    (SELECT @rownum:=0) AS R
WHERE
    a.some_column = 1
ORDER BY 1;
```

* 정렬과 row의 줄수가 몇번째인지 표시
