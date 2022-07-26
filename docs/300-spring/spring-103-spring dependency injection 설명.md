---
layout: default
title: spring dependency injection 설명
parent: spring
nav_order: 300103
---

## DI란?
* dependency injection 의존성 주입, 빈 주입
* IOC inverse of control을 구현하는 방법중 하나
* 달느 방법으로는 dependency lookup도 있음
* 각각의 계층이나 서비스들 간에 의존성이 존재할 경우 프레임워크가 서로 연결
* @Autowired로 연결 해서 사용

## Spring의 Dependency Injection 종류
1. Constructor Injection
   Spring 4.3에서 단일 생성자의 경우 @Autowired가 필요가 없다.
```java
@Component
public class ConstructorInjection {
     private final LoginService loginService;
     private final SignupService signupService;

    @Autowired
    public ConstructorInjection(LoginService loginService, 
                SignupService signupService) {
         this.loginService = loginService;
         this.signupService = signupService;
    }
}
```

2. Field Injection
```java
@Component
public  class FieldInjection {
    @Autowired
    private LoginService loginService;
    @Autowired
    private SignupService signupService;
}
```

3. Setter Injection
```java
@Component
public  class SetterInjection {
     private LoginService loginService;
     private SignupService signupService;

    @Autowired
    public  void setLoginService(LoginService loginService) {
         this.loginService = loginService;
    }

    @Autowired
    public  void setSignupService(SignupService signupService) {
         this.signupService = signupService;
    }
}
```

## 왜 Constructor Injection을 권장하나?
* 단일 책임의 원칙
   * 생성자의 인자가 많을 경우 코드량도 많아지고, 의존관계도 많아져 단일 책임의 원칙에 위배된다. 그래서 Constructor Injection을 사용함으로써 의존관계, 복잡성을 쉽게 알수 있어 리팩토링의 단초를 제공하게 된다.
* 테스트 용이성
   * DI 컨테이너에서 관리되는 클래스는 특정 DI 컨테이너에 의존하지 않고 POJO여야 한다. DI 컨테이너를 사용하지 않고도 인스턴스화 할 수 있고, 단위 테스트도 가능하며, 다른 DI 프레임 워크로 전환할 수도 있게 된다.
* Immutability
   * Constructor Injection에서는 필드는 final로 선언할 수 있다. 불변 객체가 가능한데 비해 Field Injection은 final는 선언할 수 없기 때문에 객체가 변경 가능한 상태가 된다.
* 순환 의존성
   * Constructor Injection에서는 멤버 객체가 순환 의존성을 가질 경우 BeanCurrentlyInCreationException이 발생해서 순환 의존성을 알 수 있게 된다.
* 의존성 명시
   * 의존 객체 중 필수는 Constructor Injection을 옵션인 경우는 Setter Injection을 활용할 수 있다.

### 참고링크
* spring dependency injection 종류 <https://www.baeldung.com/constructor-injection-in-spring>
* spring dependency injection 방법 <http://www.mimul.com/pebble/default/2018/03/30/1522386129211.html>
