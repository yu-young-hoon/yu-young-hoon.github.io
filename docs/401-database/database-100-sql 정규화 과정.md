---
layout: default
title: database sql 정규화 과정
parent: database
nav_order: 401100
---

## 정규화과정
* 도부이결다조 / 중복된 요소 제거과정
* 도메인 1NF 속성이 하나 정보만 묶어서 테니스, 낚시 묶어서 저장 취미1, 취미2속성으로구분
* 부분함수 2NF 일부 속성끼리 종속된 것 제거 부서, 부서명을 부서로뺌
* 이행함수 3NF 종속 a->b, b->c인 것 제거
* 결정자가 BCNF 후보키여야함, 교수 = 과목 교수가 키여야함
* 다치종속 4NF 제거 a->b, a->c  과목강사교재를 강사(과목강사) 교재(과목교재)
* 조인종속 5NF 존재, 분해후 재조립했을 때 손실이 없어야함"

### 참고링크
* 정규화 이해하기 <https://myeonguni.tistory.com/210>
* database 용어 <https://ra2kstar.tistory.com/24>
* 정규화 <https://raisonde.tistory.com/entry/%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4-%EC%A0%95%EA%B7%9C%ED%99%94Normalization%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4-%EC%A0%95%EA%B7%9C%ED%99%94Normalization>
