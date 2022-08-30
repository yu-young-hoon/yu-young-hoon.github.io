---
layout: default
title: jpa anotation 종류
parent: jpa
nav_order: 301101
---

## javax.persistence
* @Basic
* @Column

## @Transactional
* isolation = Isolation.ISOLATION_DEFAULT: default option 보통 ISOLATION_READ_UNCOMMITTED가 적용
* isolation = Isolation.READ_COMMITTED: dirty read 방지
* Propagation.REQUIRED: default option 부모 메서드가 트랜젝션이 없다면 새롭게 시작
* propagation = Propagation.REQUIRES_NEW: 새롭게 트랜젝션 시작

## @Modifying
