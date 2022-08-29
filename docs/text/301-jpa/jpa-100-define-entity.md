---
layout: default
title: entity 정의
parent: jpa
nav_order: 301100
---

* tinyint -> tinyunsigned로 지정
    * 0은 false !0은 true로 할경우 음수값을 판단하지 못하는 경우를 위함
    * 비교지정자 하나만 사용할수도 있고 디버깅이 쉬움
* Id bigint unsigned
* fk는 잡지 않더라도 연관에 관한 인덱스는 걸어주는것이 좋다
* 가격 같은 음수가 나올수 없는 형태의 값에도 unsigned를 지정 하는 것이 좋고 @Min의 어노테이션을 지정하여 네가티브 값이 들어가는것을 방지 하는것이 좋다(아래같은 문제)
    * OR aab.remain_point = 0 -- no more points
    * OR aab.remain_point < aag.cost_per_click -- not enough point
