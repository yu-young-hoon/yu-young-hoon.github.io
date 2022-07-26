---
layout: default
title: spring batch 설명
parent: spring
nav_order: 300101
---

![](/docs/attach/batch-obejct-relrationship.png)

## 지켜야 하는 점
대용량 데이터
* 배치 어플리케이션은 대량의 데이터를 가져오거나, 전달하거나, 계산하는 등의 처리를 할 수 ​​있어야 합니다.
자동화
* 배치 어플리케이션은 심각한 문제 해결을 제외하고는 사용자 개입 없이 실행되어야 합니다.
견고성
* 배치 어플리케이션은 잘못된 데이터를 충돌/중단 없이 처리할 수 있어야 합니다.
신뢰성
* 배치 어플리케이션은 무엇이 잘못되었는지를 추적할 수 있어야 합니다. (로깅, 알림)
성능
* 배치 어플리케이션은 지정한 시간 안에 처리를 완료하거나 동시에 실행되는 다른 어플리케이션을 방해하지 않도록 수행되어야합니다.

## 주의 할것
* @Bean 메소드에서 @StepScope를 사용할경우 ItemReader, ItemWriter 구현체로 bean등록할것
* ItemReader 인터페이스의 프록시 객체를 생성하여 리턴하기때문에 구현체로 지정하여야합니다.

### 참고링크
* Spring Batch 가이드 - Batch Job 실행해보기 <https://jojoldu.tistory.com/325?category=635883>
* spring batch @StepScope 사용시 주의사항 <https://jojoldu.tistory.com/132>
* spring batch querydsl <http://woowabros.github.io/experience/2020/02/05/springbatch-querydsl.html>
* spring batch schema <https://github.com/spring-projects/spring-batch/blob/master/spring-batch-core/src/main/resources/org/springframework/batch/core/schema-mysql.sql>
* spring batch StepExecutionListener aggregate 하는법 <https://gist.github.com/langmi/1673085>
