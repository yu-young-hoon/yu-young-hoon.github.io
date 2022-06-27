---
layout: default
title: Issue intellij exploded war 생성이 안되는 문제
parent: issue
nav_order: 101101
---

## intellij의 gradle이 아니라 기본 설정을 사용하게 된다면 exploded war가 생성 되지 않는 버그가 있다.
![](/docs/attach/intellij-exploded-war.png)

task를 새로 만들어서 사용거나 intellij의 내장된 gradle을 사용하면 된다.

## 참고링크 
* https://youtrack.jetbrains.com/issue/IDEA-176700