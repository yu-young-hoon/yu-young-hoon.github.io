---
layout: default
title: Spring Error local class incompatible:stream classdesc serialVersionUID = 420, local class serialVersionUID = 510
parent: error
nav_order: 102202
---

## 원인
spring security에서 공통으로 사용하는 serialVersionUID 가 버전 별로 다르기 때문에 생기는 문제입니다

```java
public static final long SERIAL_VERSION_UID = 530L;
```

## 경과
스프링 버전을 1.5.X에서 2.3.X로 올리게 되었습니다.

서버중 1대만 선반영을 시도하였습니다.

tomcat session clustering이 되어 있기 때문에 선반영한 서버와 나머지 서버간 session의 serialVersionUID 가 다르기 때문에 문제가 발생하였습니다.

## 해결
선반영된 서버 1대를 다시 이전 리비전으로 돌렸습니다.

서버 모두 한번에 반영하였고 모든 서버 반영 전에는 동일한 에러가 나오다 반영 완료 후에 더이상 같은 메시지는 나오지 않았습니다.

## 참고링크
* https://www.programmersought.com/article/62982080325/
