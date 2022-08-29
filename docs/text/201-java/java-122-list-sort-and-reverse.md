---
layout: default
title: java list sort and reverse
parent: java
nav_order: 201122
---

### List interface의 sort
```java
    someList.sort(someComparator);
```

### Collections class의 sort

```java
    Collections.sort(someList);

    Collections.sort(someList, someComparator);
```

### Comparator
* Comparator 인터페이스를 상속 받아 구현하거나 comparing static method를 사용할수 있다

### Collections reverse
```java
    Collections.reverse(someList);
```
