---
layout: default
title: JPA Error Unable to create unique key constraint not found
parent: error
nav_order: 102301
---

Entity에 유니크 DDL 속성을 주려고 uniqueConstraints 설정중 에러 발생

Unable to create unique key constraint not found 에러와 함께

database column 'xxx' not found 데이터 베이스에서 필드를 찾지 못한다고 표시 되었다

데이터 베이스에도 컬럼 이름에 id가 없지만 @UniqueConstraint(columnNames = {"xxxId"}처럼 끝에 Id를 추가해줘야 동작 하는 걸로 보아

hibernate 오류로 보이고 5.0.11이 아닌곳에서도 같은 엔티티 형태가 에러를 발생하는지 확인해봐야 할것 같다.