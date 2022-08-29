---
layout: default
title: database mysql index
parent: database
nav_order: 401210
---

## SQL Index

### index는 ascending 기본

### BTree

### super key 복합키, multiple indexes

KEY 또는 INDEX 는 일] 비 고유 색인을 나타냄니다. 인덱스에 대해 다른 값을 사용할 수 없으므로 인덱스 에는 인덱스의 모든 열에 동일한 값을 갖는 행 이 포함될 수 있습니다. 이러한 인덱스는 데이터에 제한을 두지 않으므로 특정 쿼리를 신속하게 실행할 수 있도록하기 위해 사용됩니다.

UNIQUE 는 색인의 모든 행이 고유해야하는 색인을 나타냄니다. 즉, 같은 행이이 인덱스의 다른 모든 행에 대해 동일한 비 NULL 값을 가질 수 없습니다. 데이터베이스 시스템은 데이터를 삽입하거나 업데이트 할 때이 고유 한 값 규칙이 깨지지 않도록하기 때문에 쿼리의 속도를 높이는 데 사용되는 것뿐만 아니라 UNIQUE 인덱스를 사용하여 데이터에 대한 제한을 적용 할 수 있습니다.

데이터베이스 시스템은 UNIQUE 인덱스가 NULL 값을 허용하는 열에 적용되도록 허용 할 수 있습니다.이 경우 두 열 모두 NULL 값을 포함하면 두 행이 동일하게 허용됩니다 (여기서는 NULL이 자체가 아닌 것으로 간주됩니다). 그러나 응용 프로그램에 따라 바람직하지 않을 수 있습니다.이를 방지하려면 관련 열에서 NULL 값을 허용하지 않아야합니다.

PRIMARY 는 항상 'PRIMARY'라는 이름을 제외하고는 UNIQUE 인덱스와 똑같이 작동하며 테이블에는 하나만있을 수 있습니다 ( 항상 하나의 데이터베이스 시스템 이 있어야 하지만 일부 데이터베이스 시스템에서는이를 적용하지 않습니다). PRIMARY 인덱스는 테이블의 모든 행을 고유하게 식별하는 기본 수단으로 사용되므로 UNIQUE와 달리 NULL 값을 허용하는 열에서는 사용하면 안됩니다. PRIMARY 색인은 행을 고유하게 식별하는 데 충분한 최소 수의 열에 있어야합니다. 종종 고유 한 자동 증가 숫자가 포함 된 하나의 열일 뿐이지 만 국가 목록에서 "국가 코드"와 같이 행을 고유하게 식별 할 수있는 다른 것이 있으면 그 대신 사용할 수 있습니다.

일부 데이터베이스 시스템 (예 : MySQL의 InnoDB)은 테이블의 레코드를 PRIMARY 인덱스에 나타나는 순서대로 디스크에 저장합니다.

FULLTEXT 인덱스는 위의 모든 것과 다르며 데이터베이스 시스템의 동작이 크게 다릅니다. FULLTEXT 인덱스는 위의 세 가지와 달리 MATCH () / AGAINST () 절을 사용하여 전체 텍스트 검색을하는 경우에만 유용합니다. 일반적으로 b- 트리를 사용하여 내부적으로 구현됩니다 (가장 왼쪽 열에서부터 선택, 정렬 또는 범위를 시작할 수 있음). 해시 테이블 (가장 왼쪽 열에서 시작하여 선택 가능).

다른 인덱스 유형이 범용 인 경우 FULLTEXT 인덱스는 특수 목적으로 사용됩니다. 이는 전체 텍스트 검색 기능에만 사용됩니다.

* MySQL Ascending index vs Descending index <http://tech.kakao.com/2018/06/19/AscendingAndDescendingIndex/>
* 개발자를 꿈꾸는 프로그래머 :: 키(Key)의 개념과 종류 <https://jwprogramming.tistory.com/75>
* indexing - Differences between INDEX, PRIMARY, UNIQUE, FULLTEXT in MySQL <https://stackoverflow.com/questions/707874/differences-between-index-primary-unique-fulltext-in-mysql>
* https://jdm.kr/blog/168
