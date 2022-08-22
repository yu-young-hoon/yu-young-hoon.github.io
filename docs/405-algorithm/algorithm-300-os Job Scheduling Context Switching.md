---
layout: default
title: algorithm os Job Scheduling Context Switching
parent: algorithm
nav_order: 405300
---

* FCFS 들어온거부터
* SJF 수행 시간이 짧다고 판단되는거 부터
* HRN 긴작업과 짧은 작업 보완 대기+서비스/서비스 클수록 우선순위 높음

### Write through, Write Back
파일안에 내용을 읽어 올때 동작을 cache와 관련지어 설명


### write-through
프로세서에서 메모리에 쓰기를 할때마다 캐시의 내용을 메인 메모리의 내용으로 바꿈
캐시에 의한 접근 시간 개선이 사라짐
write-back
캐시에 먼저 쓰기 작업, 변경 사실을 확인 할 수 있는 표시
캐시에서 내용이 제거 될때 메인 메모리로 복사, 더 효율이 좋음


### 문맥교환
cpu에서 동작중인 프로세스의 상태를 저장하고(pcb에)
다음 프로세스를 실행, 혹은 프로세스의 보관된 상태를 복구
이런 시간은 오버헤드임
