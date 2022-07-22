---
layout: default
title: java Lambda Expressions과 Functional Interface
parent: java
nav_order: 201109
---

### 기본 개념
* java8에서 추가 되었습니다.
* Lambda expressions(람다 표현식)이란 익명 함수를 지칭한다.
* java에서 함수형 인터페이스(method가 하나 있는 인터페이스)는 람다 표현식으로 사용할수 있다.
* 식별자 없이 실행 가능한 함수

### Thread에서 Runable을 람다식으로 사용한 예
```java
// 메서드가 하나인 함수형 인터페이스 Runable
@FunctionalInterface
public interface Runnable {
    /**
     * When an object implementing interface <code>Runnable</code> is used
     * to create a thread, starting the thread causes the object's
     * <code>run</code> method to be called in that separately executing
     * thread.
     * <p>
     * The general contract of the method <code>run</code> is that it may
     * take any action whatsoever.
     *
     * @see     java.lang.Thread#run()
     */
    public abstract void run();
}
```
* Runable interface는 함수형 인터페이스로 run이란 하나의 메서드를 가지고 있습니다.

```java
// Thread의 생성자
public Thread(Runnable target) {
    init(null, target, "Thread-" + nextThreadNum(), 0);
}
```
* Thread의 생성자에서 Runable을 파라메터로 받고 있기 때문에 람다식을 대입할 수 있습니다.

```java
// Thread의 Lambda expression 사용
new Thread(()->{
	System.out.println("Hello World.");
}).start();
```
* 함수형 인터페이스인 Runable이 익명 함수로 사용되어 람다식이 된 모습입니다.

### 자바에서 기본적으로 사용되는 함수형 인터페이스
* @FunctionalInterface 어노테이션은 함수형 인터페이스를 나타냅니다.


### 참고링크
* java project lambda <http://openjdk.java.net/projects/lambda/>
* java 8 람다 표현식 자세히 살펴보기 <https://skyoo2003.github.io/post/2016/11/09/java8-lambda-expression>
* java Consumer , Supplier, Function 함수적 인터페이스 <https://altongmon.tistory.com/245>
* java Operator , Predicate 함수적 인터페이스 <https://altongmon.tistory.com/246>
* java Functional Interfaces in Java 8 <https://www.baeldung.com/java-8-functional-interfaces>
* java 람다 표현식 <https://medium.com/@circlee7/java8-lambda-%EB%9E%8C%EB%8B%A4-%ED%91%9C%ED%98%84%EC%8B%9D%EC%9D%98-%EB%8F%99%EC%9E%91-%EC%9D%B4%ED%95%B4-cf5342eeb5ac>
