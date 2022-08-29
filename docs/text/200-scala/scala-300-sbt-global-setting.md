---
layout: default
title: Scala sbt 전역 설정
parent: scala
nav_order: 200300
---

sbt 버전의 전역 설정을 변경하고자 하였다.

/usr/local/etc/sbtopts

```yml
# Sets the SBT version to use.
sbt-version  1.5.8

# 맨 끝에 -verbose를 기입하면 적용 완료
-verbose
```