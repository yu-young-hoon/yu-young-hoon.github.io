---
layout: default
title: hibernate envers
parent: jpa
nav_order: 301102
---

## hibernate envers
* jpa entity의 이력 관리 라이브러리
* _aud 테이블에 히스토리 이력이 저장되어 따로 히스토리 관리할 필요가 없어집니다

## dependency
* gradle dependencies에 아래 내용을 추가하면 됩니다
* implementation 'org.springframework.data:spring-data-envers'

## entity 설정
@Audited 어노테이션을 Entity에 사용하면 됩니다. 기본 히스토리 테이블은 suffix에 _aud가 붙습니다.

## history 테이블 이름 변경
* @AuditTable("table 이름")으로 히스토리 테이블 이름을 지정할수 있습니다
* 프로퍼티를 바꿔서 지정할수도 있습니다. spring.jpa.properties.org.hibernate.envers.audit_table_suffix: _history

## 연관클래스 이력
@Audited(targetAuditMode = RelationTargetAuditMode.NOT_AUDITED)

## 테이블 생성
* spring.jpa.hibernate.ddl-auto: create 매번 새로 생성되니까 운영에는 사용하지 말것

```yml
plugins {
    id "org.hibernate.gradle.tools" version "1.2.5"
}
apply plugin: "hibernatetools-gradle-plugin"
```
gradle을 통해서 실행 할수도 있다

### 참고링크
* hibernate envers options <https://docs.jboss.org/hibernate/envers/3.6/reference/en-US/html/configuration.html>
