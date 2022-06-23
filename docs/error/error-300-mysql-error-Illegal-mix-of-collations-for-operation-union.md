---
layout: default
title: Mysql Error Illegal mix of collations for operation 'UNION' 쿼리 에러
parent: error
nav_order: 300
---

## 에러
* Mysql Error: Illegal mix of collations for operation 'UNION' 쿼리 에러
* union 또는 union all을 할때 컬럼의 속성이 다를때 발생하는데 charset이 달라도 발생하는듯 하다.

## 해결법
* 문제가 되는 컬럼을 변경하거나 테이블 전체의 컬럼을 바꿔주면 된다.
* ex) ALTER TABLE some_table MODIFY COLUMN `some_column` varchar(200) CHARACTER SET utf8mb4 COLLATE utf8_general_ci;