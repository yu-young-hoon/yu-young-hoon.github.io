---
layout: default
title: java 메서드 참조 연산자
parent: java
nav_order: 201117
---

### 메서드 참조 연산자 (method reference operator :: 더블 콜론)
자바에서 :: 더블 콜론 기호를 사용해서 클래스의 method를 직접 호출하는 연산자 입니다.

람다식에서 함수형 인터페이스와 동일하게 사용할수 있습니다.

* a static method.
* an instance method.
* a constructor.
  위의 3가지의 경우에 사용할수 있습니다.

```java
    // 정적 메서드
    SomeClass::staticMethod;

    // 생성자
    SomeClass obj = SomeClass::new;

    // 인스턴스의 메서드
    obj::someMethod;
```

### 참고링크
* https://www.geeksforgeeks.org/double-colon-operator-in-java/
