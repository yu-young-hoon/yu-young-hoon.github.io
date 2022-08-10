---
layout: default
title: Issue Network PKIX path validation failed
parent: issue
nav_order: 101500
---

## 이슈
url 접속시 인증서 검증 오류 발생

## 확인
curl -v https://xxx.co.kr 결과 (proxy를 통한 요청일경우 --proxy http://proxy.domain과 함께 확인)

Peer's Certificate has expired. 출력 확인

## 해결
인증서 만료로 url 소유 기관의 인증서 갱신 요청

