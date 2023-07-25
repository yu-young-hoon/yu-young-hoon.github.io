---
layout: default
title: database mysql 명령어
parent: database
nav_order: 401201
---

### 덤프파일 실행방법
* $ mysql -u admin2017 -p schema_name < /Users/we/Downloads/queries.sql

### session process 리스트 보기와 종료
* show processlist;
* kill 123;

### session에 트랜젝션 레벨 부여
* SET SESSION TRANSACTION ISOLATION LEVEL READ UNCOMMITTED;

### procedure
* 목록보기 SHOW PROCEDURE STATUS;
* 코드보기 SHOW CREATE PROCEDURE stored_procedure_name;

### index 조회
* SHOW INDEXES FROM table_name;

### 테이블 구조 조회
* DESC db_name.table_name;
