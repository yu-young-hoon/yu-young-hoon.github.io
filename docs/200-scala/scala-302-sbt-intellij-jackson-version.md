---
layout: default
title: Scala sbt intellij jackson version 문제
parent: scala
nav_order: 200302
---

## 이슈
intellij 2022.2로 idea를 변경하면서 debug로 실행했을때 

jackson-databind-2.8.9.jar가 아닌 jackson-databind-2.11.0.jar으로 실행하여 swagger를 로드할때 오류 발생

sbt로 직접 실행하면 이슈가 없는걸로 보아 idea에서 잘못 넣어주고 있는걸로 보여

## 해결
/Users/xxxx/Library/Caches/Coursier 아래 캐시를 날리고 다시 구버전 intellij 2021로 사용

## TODO
최신 idea에서 동작하게 종속성 정리 