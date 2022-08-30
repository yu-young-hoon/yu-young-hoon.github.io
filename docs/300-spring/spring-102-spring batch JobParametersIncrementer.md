---
layout: default
title: spring batch JobParameterIncrementer
parent: spring
nav_order: 300102
---

Spring batch는 job + job paramenter로 새로운 실행인지를 구분하는데

RunIdIncrementer의 경우 파라미터가 동일할때 다시 실행이 가능하도록

임의의 파라메터인 run.id 추가하고 증가시켜주는 동작이 가능하도록 합니다.

RunIdIncrementer는 new JobParametersBuilder(params) 이런 코드를 사용하는데 이전값을 복구하는 생성자를 사용하고 있기때문에

JobParametersIncrementer의 새로운 구현체 클래스를 생성하거나 람다 메서드를 만들어 사용해야 재실행이 가능하도록 할수 있다.


### 참고링크
* https://jojoldu.tistory.com/487
* https://github.com/codecentric/spring-boot-starter-batch-web/issues/38
