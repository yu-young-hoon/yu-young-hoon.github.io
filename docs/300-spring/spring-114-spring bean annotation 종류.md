---
layout: default
title: spring bean annotation 종료
parent: spring
nav_order: 300114
---

## component
```java
@Component
public class SomeClass {

}
```
* 가장 기본이 되는 클래스를 Bean으로 등록해주는 Annotation

## configuration
```java
@Configuration
public class SomeClass {
    @Bean
    public SomeClass getSomeClass() {
        return new SomeClass();
    }
}
```
* 외부 클래스를 대신 Bean으로 등록 해주는 Annotation
