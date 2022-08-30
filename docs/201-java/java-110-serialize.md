---
layout: default
title: java serialize
parent: java
nav_order: 201110
---

implements Serializable

private static final long serialVersionUID = 1L;

SUID(serialVersionUID) 필수 값은 아니다.

호환 가능한 클래스는 SUID값이 고정되어 있다.

SUID가 선언되어 있지 않으면 클래스의 기본 해쉬값을 사용한다. (해쉬값 알고리즘은 링크에서 확인이 가능합니다.)

jsonIgnore의 경우 jackson종속적 entity자체가 직렬화 되는것 자체가 문제 사용하면 안됨.

tostring exclude의 경우 로그로 찍는등의 경우가 있기 때문에 사용할 수도 있음

### 참고링크
* java 직렬화 <http://woowabros.github.io/experience/2017/10/17/java-serialize.html>
