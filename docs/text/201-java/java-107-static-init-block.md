---
layout: default
title: java static 초기화 블럭
parent: java
nav_order: 201107
---

```java
class SomeClass {

    static { }    // 클래스 초기화 블럭

    { }           // 인스턴스 초기화 블럭

}
```

* 클래스 초기화 블럭: 클래스 변수의 복잡한 초기화에 사용된다. 클래스가 처음 로딩될 때 한번만 수행된다.
* 인스턴스 초기화 블럭: 인스턴스 변수의 복잡한 초기화에 사용된다. 인스턴스가 생성될때 마다 수행된다. (생성자보다 먼저 수행된다.)
