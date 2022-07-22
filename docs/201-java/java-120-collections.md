---
layout: default
title: java collection 모음
parent: java
nav_order: 201120
---

### Collection Framework
* ![](/docs/attach/java-collections2.jpeg)
* 모든 콜렉션의 상위 인터페이스로써 콜렉션들이 갖고 있는 핵심 메소드를 선언
* (add, contain, isEmpty, remove, size, iterator ...)
  ! 인터페이스 ! 구현클래스                          ! 특징 !
  | List   | LinkedList Stack Vector ArrayList | 순서가 있는 데이터의 집합, 데이터의 중복을 허용한다.|
  | Set    | HashSet TreeSet                   | 순서를 유지하지 않는 데이터의 집합, 데이터의 중복을 허용하지 않는다.   |
  | Map    | HashMap TreeMap\\                 | key와 value의 쌍으로 이루어진 데이터의 집합 |
  |        | HashTable Properties              | 순서는 유지되지 않고, 키는 중복을 허용하지 않으며 값의 중복을 허용한다.|

### List Interface
* Collection 인터페이스를 확장한 자료형으로 요소들의 순서를 저장하여 색인(Index)를 사용하여 특정 위치에 요소를 삽입하거나 접근할 수 있으며 중복 요소 허용
* ArrayList
  ** 상당히 빠르고 크기를 마음대로 조절할 수 있는 배열
  ** 단방향 포인터 구조로 자료에 대한 순차적인 접근에 강점이 있음
* Vector
  ** ArrayList의 구형버전이며, 모든 메소드가 동기화 되어있음 잘 쓰이진 않음
* LinkedList
  ** 양방향 포인터 구조로 데이터의 삽입, 삭제가 빈번할 경우 빠른 성능을 보장.
  ** 스택, 큐, 양방향 큐 등을 만들기 위한 용도로 쓰임

### Set Interface
* 집합을 정의하며 요소의 중복을 허용하지 않음. 상위 메소드만 사용함
* HashSet
  ** 가장 빠른 임의 접근 속도
  ** 순서를 전혀 예측할 수 없음
* LinkedHashSet
  ** 추가된 순서, 또는 가장 최근에 접근한 순서대로 접근 가능
* TreeSet
  ** 정렬된 순서대로 보관하며 정렬 방법을 지정할 수 있음

### Map Interface
* Key와 Value의 쌍으로 연관지어 저장하는 객체
* HashMap
  ** Map 인터페이스를 구현하기 위해 해시테이블을 사용한 클래스
  ** 중복을 허용하지 않고 순서를 보장하지 않음
  ** 키와 값으로 null이 허용
* Hashtable
  ** HashMap 보다는 느리지만 동기화가 지원
  ** 키와 값으로 null이 허용되지 않음
* TreeMap
  ** 이진검색트리의 형태로 키와 값의 쌍으로 이루어진 데이터를 저장
  ** 정렬된 순서로 키/값 쌍을 저장하므로 빠른 검색이 가능
  ** 저장시 정렬(오름차순)을 하기 때문에 저장시간이 다소 오래 걸림
* LinkedHashMap
  ** 기본적으로 HashMap을 상속받아 HashMap과 매우 흡사
  ** Map에 있는 엔트리들의 연결 리스트를 유지되므로 입력한 순서대로 반복 가능


## 초기화 하며 추가
```java
Set<String> h = new HashSet<String>() {{
    add("a");
    add("b");
}};
```
