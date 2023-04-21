---
layout: default
title: git branching models 종류
parent: git
nav_order: 700112
---

## Git Flow

## GitHub Flow
* Master branc의 모든 지점은 배포가 가능해야한다.
* 새로운 작업은 마스터에서 생성되고 설명이 될수 있는 이름을 줘야한다(new-oauth2-scopes)
* 커밋은 로컬과 원격에 동일하게 push해야한다.
* 피드백 또는 도음이 필요하거나 병합될 준비가 되었다면 pull request를 열어라
* 리뷰가 종료되고 사인오프되면 master로 병합한다.
* 마스터로 병합되었으면 즉시 배포 가능해야 하고 배포 해야한다.
  ===장점===
* 지속적인 통합에 알맞다
* 깃 플로우보다 간단하다
* 싱글 버전으로 진행되는 프로젝트에 알맞다

## GitLab flow
