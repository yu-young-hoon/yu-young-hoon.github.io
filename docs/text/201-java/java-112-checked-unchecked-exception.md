---
layout: default
title: java checked exception unchecked exception
parent: java
nav_order: 201112
---

### checked exception
* 예외처리 필요
* 트랜젝션 기본 롤백 안됨
* IOException, SQLException

### unchecked exception
* 예외처리 하지 않아도 빌드 진행
* 트랜젝션 기본 롤백
* NullPointerException, IllegalArgumentException
* RuntimeException을 상속한 Exception 상속 클래스

### 참고링크
* Checked, UnChecked Exception 차이 <https://cheese10yun.github.io/checked-exception/>
