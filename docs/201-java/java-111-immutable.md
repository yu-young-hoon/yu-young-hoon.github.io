---
layout: default
title: java Immutable
parent: java
nav_order: 201111
---

### 불변객체
* 속성이 변경 되지 않는 객체
* 대입 연산시 새로운 객체로 변경

### Immutable Cache
Cache 객체가 되는것은 Immutable해야 안전함


### Immutable 클래스
String, Boolean, Integer, Float, Long

Heap 영역의 값이 바뀌는 것이 아니라 영역의 객체가 바뀌도록 재할당 됨

### 함수형 프로그래밍의 핵심원리
* 객체의 레퍼런스를 통해 객체를 변경하기 때문에 문제가 발생
* defensive copy를 통해 새로운 객체를 생성한후 변경 또는 Observer패턴으로 객체 변경에 대처
* 함수형 프로그래밍의 4가지 키워드 enumerate, map, filter, accumulate

### 참고링크
* 자바에서 Immutable이 뭔가 <https://hashcode.co.kr/questions/727/%EC%9E%90%EB%B0%94%EC%97%90%EC%84%9C-immutable%EC%9D%B4-%EB%AD%94%EA%B0%80%EC%9A%94>
* 객체와 변경불가성 <https://poiemaweb.com/js-immutability>
