---
layout: default
title: java Collections.emptyList vs new ArrayList
parent: java
nav_order: 201115
---

```java
    @SuppressWarnings("rawtypes")
    public static final List EMPTY_LIST = new EmptyList<>();

    @SuppressWarnings("unchecked")
    public static final <T> List<T> emptyList() {
        return (List<T>) EMPTY_LIST;
    }
```
* java.util의 Collections에 있는 emptyList를 호출 하게 되면 이미 생성된 EmptyList 인스턴스를 꺼내줍니다
* static final로 선언 되었기 때문에 new ArrayList와 같이 인스턴스를 새로 생성 하지 않고 immutable(불변한) 인스턴스를 꺼내주게 됩니다


```java
    static <E> List<E> of​()
```
* java9에서는 List.of() 함수가 추가되었고 Collections.emptyList()와 동일한 동작을 합니다
