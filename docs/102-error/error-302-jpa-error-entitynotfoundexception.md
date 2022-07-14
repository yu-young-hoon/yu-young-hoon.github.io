---
layout: default
title: JPA Error EntityNotFoundException
parent: error
nav_order: 102302
---

* 조인 관계에서 엔티티가 매핑이 되지 않을때 EntityNotFoundException 발생
* 찾지 못할때 무시하는 어노테이션 설정

`@NotFound(action = NotFoundAction.IGNORE)`

### 참고링크
* https://stackoverflow.com/questions/13539050/entitynotfoundexception-in-hibernate-many-to-one-mapping-however-data-exist/13558787
