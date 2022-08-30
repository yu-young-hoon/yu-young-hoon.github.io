---
layout: default
title: java reflection 설명
parent: java
nav_order: 201104
---

* Reflection(리플렉션, 투영, 반사)
  ** 리플렉션이란 객체를 통해 클래스의 정보를 분석하는 기법이다.
  ** 리플렉션은 객체의 구조에 대해 동적 검색을 런타임에서 지원한다.
  ** 리플렉션은 클래스 타입을 알지 못해도, 그 클래스의 메소드, 타입, 변들들을 접근할 수 있도록 해주는 Java API 이다.
  ** 자바 클래스 파일은 바이트 코드로 컴파일되어 Static 영역에 위치하게 된다. 클래스 이름만 안다면, 바이트 코드를 뒤져 클래스에 대한 정보를 가져올 수 있다.


* 클래스타입, 메소드, 생성자 등을 조회해서 사용가능하다
  ** ClassName
  ** Class Modifiers(접근제한자 synchronized등)
  ** Package info
  ** Superclass
  ** Implemented Interfaces
  ** Constructors
  ** Methods fields
  ** Annotations


* 스피링에서 빈 팩토리로 객체 호출 될때 객체의 인스턴스를 생성할때 사용
* 자바에는 동적으로 객체를 생성하는 기술이 없기 때문에 리플렉션으로 역할을 대신함
* 데이터를 시리얼라이즈 하거나 전송할때 클래스 구조 파악해서 사용할때에도 사용

```java
// 클래스에서 클래스 타입 조회
Class c = Data.class;

// 클래스 이름에서 클래스타입 조회
Class c = Class.forName("클래스이름");

// 메소드 가져오기
Method[] m = c.getMethods();

// 변수 가져오기
Field[] f = c.getFields();

// 생성자 가져오기
Constructor[] cs = c.getConstructors();

// 인터페이스
Class[] inter = c.getInterfaces();

// 부모 클래스
Class superClass = c.getSuperclass();
```

### 참고링크
* https://docs.oracle.com/javase/8/docs/technotes/guides/reflection/proxy.html
* https://www.baeldung.com/java-dynamic-proxies
* https://www.baeldung.com/java-reflection-class-fields
