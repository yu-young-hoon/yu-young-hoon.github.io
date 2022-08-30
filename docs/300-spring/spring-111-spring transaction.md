---
layout: default
title: spring transaction
parent: spring
nav_order: 300111
---

propergation new의 경우 servcie를 호출하는 상위 서비스 중간에서 동작하기 때문에

controller까지 Exception을 던지지 않고 service까지 던지면 aop가 동작함

propagation required new

### 참고링크
* spring transaction 속성 <https://springsource.tistory.com/136>
* spring transaction 옵션 <https://taetaetae.github.io/2016/10/08/20161008/>
* spring transaction 설명 <https://goddaehee.tistory.com/167>
* spring transaction 속성 <https://habr.com/en/post/513644/>
* transaction isolate <https://habr.com/en/post/513644/>
* transaction exception <http://woowabros.github.io/experience/2019/01/29/exception-in-transaction.html>
* spring transaction이 동작하지 않는 경우 <https://netframework.tistory.com/entry/Spring-Transactional%EC%97%90-%EB%8C%80%ED%95%98%EC%97%AC>
