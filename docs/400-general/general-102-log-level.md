---
layout: default
title: General 로그 레벨 log level
parent: general
nav_order: 400102
---

## 로그 레벨 log level
Java Loggin Framework에는 log4j, log4j2, logback 등이 있고 다음과 같은 로그 레벨을 가진다.

## 로그 레벨 종류
* FATAL : 아주 심각한 에러가 발생한 상태를 나타낸다.
* ERROR : 어떠한 요청을 처리하는 중 문제가 발생한 상태를 나타낸다. 프로그램 동작에 큰 문제가 발생했다는 것으로 즉시 문제를 조사해야 하는 것 (DB를 사용할 수 없는 상태, 중요 에러가 나오는 상황)
* WARN : 프로그램의 실행에는 문제가 없지만, 향후 시스템 에러의 원인이 될 수 있는 경고성 메시지를 나타낸다. WARN에서도 2가지의 부분에선 종료가 일어남
  * 명확한 문제 : 현재 데이터를 사용 불가, 캐시값 사용 등
  * 잠재적 문제 : 개발 모드로 프로그램 시작, 관리자 콘솔 비밀번호가 보호되지 않고 접속 등
* INFO : 어떠한 상태 변경과 같은 정보성 메시지를 나타낸다.
* DEBUG : 개발시 디버그 용도로 사용하는 메시지를 나타낸다.
* TRACE : 디버그 레벨이 너무 광범위한 것을 해결하기 위해서 좀 더 상세한 이벤트를 나타낸다. 

## 로그 레벨 노출 순서
* TRACE > DEBUG > INFO > WARN > ERROR > FATAL
* 로그레벨을 설정할때 낮은 로그레벨을 설정하면 그 상위 레벨의 로그는 모두 포함한다.
* INFO로 셋팅하면, INFO, WARN, ERROR, FATAL이 기록된다.
* WARNG로 셋팅하면, WARN, ERROR, FATAL이 기록된다.

### 참고링크
* <https://pig-programming.tistory.com/51>
* <https://shplab.tistory.com/entry/log4j-vs-logback-vs-log4j2>
