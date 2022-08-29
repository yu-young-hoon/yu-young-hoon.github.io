---
layout: default
title: Issue jpa @NotFound(action=NotFoundAction.IGNORE) n+1
parent: issue
nav_order: 101201
---

@NotFound(action=NotFoundAction.IGNORE)을 사용하여 EntityNotFoundException을 회피하려고 할때
에러는 발생하지 않지만 해당 필드는 다시 select를 호출하여 n+1을 발생시킨다
