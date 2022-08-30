---
layout: default
title: spring security 설명
parent: spring
nav_order: 300108
---

## UserDetailsService vs AuthenticationProvider
* userName으로 UserDetail을 불러오려면 UserDetailsService interface를 구현 하면된다.
* 비밀번호등 로직을 따로 구현하려면 AuthenticationProvider 구현하면 된다.

## @EnableGlobalMethodSecurity
```java
// method 제약 어노테이션 활성화
@EnableGlobalMethodSecurity(securedEnabled = true, prePostEnabled = true)
public class WebSecurityConfig {
    ....
}

interface someInterface {
    @Secured("ROLE_TELLER")       // 역할 기반 method 제약
    public Account readAccount(Long id);

    @PreAuthorize("isAnonymous2()")    // 표현식 기반 method 제약
    public Account readAccount(Long id);

    @PreAuthorize("hasRole(T(full.identifier.AuthRole).ADMIN.getRole())")    // 표현식 기반 method 제약
    public Account readAccount3(Long id);
}
```

## 참고링크
* spring security 설명 <https://okky.kr/article/382738>
* spring security 구조 <https://minwan1.github.io/2017/03/25/2017-03-25-spring-security-theory/>
* spring security EL custom <https://springboot.cloud/12>
