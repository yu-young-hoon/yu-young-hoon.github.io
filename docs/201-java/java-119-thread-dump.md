---
layout: default
title: java Thread Dump 쓰레드 덤프 생성 방법
parent: java
nav_order: 201119
---

## 종류
쓰레드 덤프 생성 방법은 여러가지 종류가 있습니다.
* kill -3 옵션
* JDK의 jstack
* 등등...

## 차이
메모리 leak과 같은 문제가 발생할때 덤프를 생성해서 확인할수 있는데 kill -3이 좀더 가볍기 때문에 CPU부하가 심할때 jstack보다 좀 더 낫습니다.

jstack의 경우 java5 이상 윈도우즈의 경우는 6이상의 JDK에 포함되어 있습니다.

## 사용법
```java
$ kill -3 <pid>

$ jstack <pid> <fileName>
```
