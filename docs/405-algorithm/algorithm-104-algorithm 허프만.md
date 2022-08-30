---
layout: default
title: algorithm 허프만
parent: algorithm
nav_order: 405104
---

```html
AABBAC
A가 3번 B가 2번 C가 1번 6byte 문자열
A에 0 B에 01 C에 10
000101010으로 9bit = 1byte + 1bit으로 압축
CDDCACBCBCCCBBCDA
2A 4B 8C 3D => 8C 4B 3D 2A
8C 4B 5DA => 8C 5DA 4B
8C 9DAB => 9DAB 8C
17DABC

2진 트리를 만들어서 위에서부터 해당 문자열 까지 타고가며 비트 표현
복호화의 경우 트리를 가지고 위에서 따라가며 복호화
```