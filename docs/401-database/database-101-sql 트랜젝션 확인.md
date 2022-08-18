---
layout: default
title: database sql transaction 확인
parent: database
nav_order: 401101
---

```sql
START TRANSACTION;
SELECT @A:=SUM(salary) FROM table1 WHERE type=1;
UPDATE table2 SET summary=@A WHERE type=1;
COMMIT;
```

### 참고링크
* select로 update시 주의할 점 transaction 읽기 <https://m.blog.naver.com/parkjy76/220588832494>
