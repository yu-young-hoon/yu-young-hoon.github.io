---
layout: default
title: database mysql lock
parent: database
nav_order: 401204
---

### Shared Lock(공유 Lock 또는 Read Lock)

### Exclusive Lock(배타적 Lock 또는 Write lock)

긍정락

부정락

Blocking 레이스 컨디션

Lock 레벨이 낮을 수록 동시성이 좋아지지만, 관리해야할 Lock이 많아지기 때문에 메모리 효율성은 떨어집니다. 반대로 Lock레벨이 높을 수록 관리리소스는 낮지만, 동시성은 떨어집니다

### 참고링크
* Lock이란 <https://medium.com/@chrisjune_13837/db-lock-%EB%9D%BD%EC%9D%B4%EB%9E%80-%EB%AC%B4%EC%97%87%EC%9D%B8%EA%B0%80-d908296d0279>
* mysql lock에 관하여 <https://www.letmecompile.com/mysql-innodb-lock-deadlock/>
