---
layout: default
title: JPA Error native query pagenation
parent: error
nav_order: 102303
---

* spring data jpa 버전이 낮은경우 native query를 사용했을때 실행시 문제가 발생하게 되는데 파라매터를 주석으로 감싸서 처리하면 된다.
* spring boot 2.0.4 이상으로 업그레이드를 할경우 문제가 사라진다고 한다.

`"     /*#pageable*/",`

==참고링크==
* DATAJPA-928 NativeQuery with Pagination validation error at startup <https://jira.spring.io/browse/DATAJPA-928>
