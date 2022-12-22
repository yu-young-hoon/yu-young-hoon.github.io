---
layout: default
title: database mysql 트렌잭션 테스트
parent: database
nav_order: 401212
---

## 트랜잭션 쿼리
* 여러 단계의 쿼리를 묶고 싶을때 트랜잭션을 사용하게 되는데 SQL문에서 직접 트랜잭션을 테스트 해볼때는 start transaction로 시작을하면된다.
* 반영을 하고자 할때는 commit;을 롤백을하여 취소 하고자 할때는 rollback;으로 끝마치면 된다.

```sql
start transaction;
-- some query
commit;


start transaction;
-- some query
rollback;
```