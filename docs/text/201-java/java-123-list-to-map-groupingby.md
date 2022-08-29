---
layout: default
title: java list to map groupingBy
parent: java
nav_order: 201123
---

List<V>의 형태를 Map<K, List<V>>로 바꾸고 싶을때가 있다

이때 Collectors의 groupingBy를 사용하면 원하는 형태로 바꿀수 있다

```java
public Map<String, List<SomeDto>> getMap(List<SomeDto> strings) {
    return strings.stream().collect(
      Collectors.groupingBy(SomeDto::SomeKey)
    );
}
```

### 참고링크
* https://stackoverflow.com/questions/40772997/how-to-convert-listv-into-mapk-listv-with-java-8-streams-and-custom-list
