---
layout: default
title: Scala Iterators의 반복문이 동작 하지 않을때 Iterators Laziness
parent: scala
nav_order: 1
---

Scala에서 List와 같은 concreate collection과 달리 Interator의 map은 지연동작합니다. 결과를 바로 계산하지 않기 때문에 기대하는 결과대로 동작하지 않습니다


```scala
(1 to 10).iterator.map(println)
```
위와 같은 코드는 아무런 값도 출력하지 않습니다.


```scala
(1 to 10).iterator.map(println).toList
```
하지만 위의  코드는 1~10까지의 값을 출력합니다.

이처럼 map, filter, fold와 같은 메서드의 인수로 순수함수를 사용하는 이용하는 부작용이 발생하지 않기 때문이고
println을 위의 코드에서 사용한 이유는 lazy함을 보여주기 위해 사용하였고 일반적인 순수 함수로 prinln을 사용하진 않습니다.

참고링크
* https://docs.scala-lang.org/overviews/collections-2.13/iterators.html#laziness
