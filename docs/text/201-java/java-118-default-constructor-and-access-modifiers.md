---
layout: default
title: java default constructor and access modifiers 기본 생성자와 접근 제한자
parent: java
nav_order: 201118
---

## access modifiers 접근 제한자
자바의 접근 제한자는 4가지가 있습니다
* public
* protected
* default(package-private)
* private

### private
같은 클래스 허용

### default(package-private)
명시적으로 접근 제한자를 두지 않는 경우를 말합니다

같은 클래스, 같은 패키지 허용

### protected
같은 클래스, 같은 패키지, 상속 했다면 다른 패키지

### public
모든 클래스, 모든 패키지


## 기본 생성자

### 기본 생성자 원리
생성자를 명시적으로 만들어 놓지 않는다면 compiler는 기본 생성자를 생성합니다

```java
// 작성한 코드
Car {}

// compiler는 기본 생성자를 많들어 줍니다
        Car {
        Car() {}
        }
```

### 기본 생성자의 접근 제한자
기본 생성자의 접근 제한자는 클래스의 접근 제한자와 동일하게 생성됩니다
* public 클래스의 기본 생성자의 접근 제한자는 public 입니다
* protected 클래스의 기본 생성자의 접근 제한자는 protected 입니다
* 클래스의 접근 제한자가 없다면 기본 생성자의 접근 제한자 또한 없습니다
* private 클래스의 기본 private 접근 제한자는 private 입니다

### 참고링크
* http://www.corejavaguru.com/java/oop/constructor
