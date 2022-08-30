---
layout: default
title: algorithm os memory page switching
parent: algorithm
nav_order: 405301
---

LRU 캐싱 2(least recently used) 오랫동안 사용되지 않은거 제거
LFU 횟수 호출된 빈도가 적은것
오랫동안 참조 되지 않을 페이지 최적교체 OPT 실현 불가
선입 선출 먼저 들어온것 교체

###CPU 처리 방식
RR 라운드 로빈 동일시간
SRT 가장 짧은 프로세스 처리
MLQ 작업을 다섯캐로
MFQ 서로 다른 타임 슬레이스 부여
