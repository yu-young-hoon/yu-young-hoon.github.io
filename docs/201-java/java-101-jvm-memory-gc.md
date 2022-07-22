---
layout: default
title: java jvm 메모리 구조, GC 설명
parent: java
nav_order: 201101
---

* JVM이 가비지 컬렉션을 실행하기 위해 stop-the-world를 발생 어플리케이션을 멈춤
* GC튜닝이란 이시간을 줄이는것

### GC 설명
가비지 컬렉터는 필요 없는 객체를 찾아서 jvm이 지우는것
명시적으로 객체를 null로 지정하는것은 문제가 되지 않지만
System.gc() 를 통해 호출하는 것은 문제가 됨
jstat -gc <vmid> 1000 : gc 정보
gc가 0.1~03.이면 괜찮음
OutOfMemoryError가 나타나거나 gc가 1초이상이면 개선
FGCT/FGC가 1초이상, 10분마다면 문제 YGCT/YGC 0.05초이상 10초마다 문제
NewRatio를 2~4로 클수록 New 작아짐
young generation 영역은 새롭게 생성한 객체
객체가 사라질때 Minor GC가 발생
young의 eden영역에서 살아 남은 것은 survivor 영역으로
survivor가 꽉차면 살아남은 것을 다른 survivor로 꽉찬것은 비우게 됨.
반복하다가 old로 이동
bump-the-pointer 마지막 eden 기록 다음 객체가 eden에 넣기 적당한지 확인 빠르게 마지막을 확인 가능
TLABs lock을 방지하기 위해 eden이 작은 덩어리로 쪼게 락없이 가능
old generation 영역은 Young에서 살아남은 객체가 복사
크기가 크며 GC는 적게 발생 객체가 사라질때 Major(full) GC 발생
old에는 512byte의 카드 테이블로 young 참조
young은 카드 테이블만 뒤져서 gc대상인지 식별
카드 테이블은 write barrier를 가져 오버헤드는 있지만
minor gc시간을 줄임

### GC 종류
* Serial GC
  ** -XX:+UseSerialGC
  ** 싱글 코어 mark-sweep-compact--
  ** old 살아있는것 식별, heap 앞부분확인 살아있는것 남기고, heap 앞부분부터 채워서 객체 존재, 없는 부분 나눔

* Parallel GC
  ** -XX:+UseParallelGC
  ** 멀티 스레드
  ** Compaction 메모리 압축하기 때문에 느림

* Parallel Old GC
  ** -XX:+UseParallelOldGC
  ** Mark-Summary-Compaction
  ** 앞서 GC 수행한 영역에 대해 별도로 살아있는것 식별, 좀더 복잡

* CMS GC
  ** -XX:+UseConcMarkSweepGC
  ** Low Latency GC
  ** serial gc에서 첫 mark때 찾는것만으로 끝네고
  ** concurrent mark에서 객체를 따라가서 참조가 끊긴것 확인
  ** concurrent sweep에서 정리작업
  ** 첫 마크만 멈추고 나머지는 다른 스레드와 동시 작업 빠르지만 메모리 많음
  ** 메모리 단편화, 메모리 모으는 작업이 많다면 worst될수 있음

* G1 GC
  ** -XX:+UseG1GC
  ** 바둑판 모양 old로 옮기지 않음, 빠름
  ** permanent generation 영역은 객체나 억류된 문자열 정보 저장
  ** GC발생하면 Major GC 횟수에 포함 Method Area라고 함

### Options
* heap
  ** -Xms 힙 시작 크기, -Xmx 최대 크기 필수 지정

* New
   ** -XX:NewRatio NewOld비율 성능에 영향 많음 1/(NewRatio + 1) New 영역
   ** -XX:NewSize New 크기
   ** -XX:SurvivorRatio Eden 영역, Survivor 영역 비율

* perm(OutOfMemoryError발생 할때만지정)
  ** -XX:PermSize
  ** -XX:MaxPermSize

```html
-Xms2g
-Xmx2g
-XX:+UseG1GC
-XX:ReservedCodeCacheSize=240m
-XX:+UseCompressedOops
-Dfile.encoding=UTF-8
-XX:SoftRefLRUPolicyMSPerMB=50
-ea
-XX:CICompilerCount=2
-Dsun.io.useCanonPrefixCache=false
-Djava.net.preferIPv4Stack=true
-Djdk.http.auth.tunneling.disabledSchemes=""
-XX:+HeapDumpOnOutOfMemoryError
-XX:-OmitStackTraceInFastThrow
-Djdk.attach.allowAttachSelf
-Dkotlinx.coroutines.debug=off
-Djdk.module.illegalAccess.silent=true
-Xverify:none
-XX:ErrorFile=$USER_HOME/java_error_in_idea_%p.log
-XX:HeapDumpPath=$USER_HOME/java_error_in_idea.hprof
```

### 참고링크
* JVM 메모리 구조 <https://12bme.tistory.com/382> 
