---
layout: default
title: oop solid 란
parent: oop
nav_order: 406101
---

{| class="wikitable" style="width: auto; font-size: 95%; table-layout: fixed; line-height:1.25; margin-left: auto; margin-right: auto;"
|-
! 두문자 !! 약어 !! 개념
|-
! S
| [[단일 책임 원칙|SRP]]
|
; [[단일 책임 원칙|단일 책임 원칙 (Single responsibility principle)]]
: 한 [[클래스 (컴퓨터 과학)|클래스]]는 하나의 책임만 가져야 한다.
|-
! O
| [[개방-폐쇄 원칙|OCP]]
|
; [[개방-폐쇄 원칙|개방-폐쇄 원칙 (Open/closed principle)]]
: “소프트웨어 요소는 확장에는 열려 있으나 변경에는 닫혀 있어야 한다.”
|-
! L
| [[리스코프 치환 원칙|LSP]]
|
; [[리스코프 치환 원칙|리스코프 치환 원칙 (Liskov substitution principle)]]
: “프로그램의 [[객체]]는 프로그램의 정확성을 깨뜨리지 않으면서 하위 타입의 인스턴스로 바꿀 수 있어야 한다.” [[계약에 의한 설계]]를 참고하라.
|-
! I
| [[인터페이스 분리 원칙|ISP]]
|
; [[인터페이스 분리 원칙|인터페이스 분리 원칙 (Interface segregation principle)]]
: “특정 클라이언트를 위한 인터페이스 여러 개가 범용 인터페이스 하나보다 낫다.”<ref name="martin-design-principles">[http://www.objectmentor.com/resources/articles/Principles_and_Patterns.pdf “Design Principles and Design Patterns”] {{웨이백|url=http://www.objectmentor.com/resources/articles/Principles_and_Patterns.pdf |date=20150906155800 }}, [[로버트 마틴]]</ref>
|-
! D
| [[의존관계 역전 원칙|DIP]]
|
;[[의존관계 역전 원칙|의존관계 역전 원칙 (Dependency inversion principle)]]
: 프로그래머는 “추상화에 의존해야지, 구체화에 의존하면 안된다.”<ref name="martin-design-principles"/> [[의존성 주입]]은 이 원칙을 따르는 방법 중 하나다.
|}


* SRP: 단일책임의 원칙(Single Responsibility Principle)
  **한 클래스는 하나의 책임만 가져야 한다.
* OCP: 개방폐쇄의 원칙(Open Close Principle)
  **소프트웨어 요소는 …… 확장에는 열려 있으나 변경에는 닫혀 있어야 한다.
* LSP: 리스코브 치환의 원칙(The Liskov Principle)
  **프로그램의 객체는 프로그램의 정확성을 깨뜨리지 않으면서 하위 타입의 인스턴스로 바꿀 수 있어야 한다.
  **계약에 의한 설계를 참고하라. 객체는 깨짐 없이 하위 클래스로 치환 될수 있어야한다, 부모의 기능을 자신은 다 구현해야한다.
* ISP: 인터페이스 분리의 원칙(Interface Segregation Principle)
  ** 특정 클라이언트를 위한 인터페이스 여러 개가 범용 인터페이스 하나보다 낫다.
* DIP: 의존성역전의 원칙(Dependency Inversion Principle)
  ** 프로그래머는 “추상화에 의존해야지, 구체화에 의존하면 안된다.”
  ** 의존성 주입은 이 원칙을 따르는 방법 중 하나다.

* 여러분의 소프트웨어가 고객이 원하는 기능을 하도록 하세요.
* 객체지향 기본원리를 적용해서 소프트웨어를 유연하게 하세요.
* 유지보수와 재사용이 쉬운 디자인을 위해 노력하세요.

=== 참고 링크 ===
* [http://www.nextree.co.kr/p6960/ 객체지향 개발 5대 원리: SOLID]
  & [http://mon.moberan.com/?p=597 oop solid 외 원칙]
* [https://www.youtube.com/watch?v=60lLSe1phks&list=PLuLb6MC4SOvXCRePHrb4e-EYadjZ9KHyH 클린 코더스 강의 OOP]
* [https://sesok808.tistory.com/31 객체지향 특징 추상화 캡슐화 상속 다형성]
* [https://epicdevsold.tistory.com/m/177 상속 2가지 서브클래싱 서브타이핑]
