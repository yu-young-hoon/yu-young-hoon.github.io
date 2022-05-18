---
layout: default
title: Scala 스칼라로 배우는 함수형 프로그래밍
parent: scala
nav_order: 200
---

# 1부 함수형 프로그래밍 입문


## 1 함수형 프로그래밍이란 무엇인가?
functional programming이란 side effect가 없는 pure function들로만 구축한다.

side effect란?
* 변수를 수정한다.
* 자료구조를 제자리에서 수정한다.
* 개게의 필드를 설정한다
* 예외를 던지거나 오류를 내면서 실행을 중단한다.
* 콘솔에 출력하거나 사용자의 입력을 읽어들인다.
* 파일에 기록하거나 파일에서 읽어들인다.
* 화면에 그린다.

modularity가 증가하기 때문에 순수 함수는 검사, 재사용, 병렬화, 일반화, 분석이 쉽고 버그가 적다.

referential transparency(참조 투명성), substitution model(치환 모델) 이라는 개념을 알아보자.

### 1.1 FP의 이점: 간단한 예제 하나
#### 1.1.1 부수가 있는 프로그램
```scala
class Cafe {
  def buyCoffee(cc: CreditCard): Coffee {
    val cup = new Coffee()
    cc.charge(cup.price)  // side effect 신용카드를 실제로 청구한다.
    cup
  }
}
```
이 함수는 Coffee 객체를 돌려줄 뿐이여야 한다.
CreditCard에서 신용카드 회사와 연동하는 방법에 대한 지식을 넣는 것은 좋지 않다.
Payments 객체를 buyCoffee에 전달한다면 코드의 모듈성과 검사성을 높일수 있다.

```scala
class Cafe {
  def buyCoffee(cc: CreditCard, p: Payments): Coffee = {
    val cup = new Coffee()
    p.charge(cc, cup.price) // side effect 하지만 검사성은 높아졌다.
    cup
  }
}
```
Payments를 인터페이스로 만들고 moc 구현을 작성하면 검사를 수월하게 진행할 수 있다.
charge 호출에 의해 상태가 변경이 되었는지 확인해야하기 때문에 어색하다.
또한 재사용하기 힘들다. 12잔의 커피를 주문한다면 buyCoffee를 12번 호출해야한다.
buyCoffees를 구현 하면 되겠지만 복잡할경우 재사용성과 합서 능력에 해가 된다.


##### 1.1.2 함수적 해법: 부수 효과의 제거
```scala
class Cafe {
  def buyCoffee(cc: CreditCard): (Coffee, Charge) = {
    val cup = new Coffee()
    (cup, Charge(cc, cup.price)) // 커피, 청구 금액 쌍을 쉼표와 괄호로 감싸 만들었다.
  }
}
```
buyCoffee가 커피뿐만 아니라 청구건을 하나의 값으로 돌려주게 하는 방법으로 수정하였다.
청구 금액을 신용카드 회사에 보내고 결과를 기록하는 등의 처리 문제등의 concern(우려)는 바깥 어딘가에서 해결하도록 한다.
청구건을 생성하는 문제와 처리, 연동의 문제가 분리되었고 함수를 재사용하기 쉬워졌다.

```scala
case class Charge(cc: CreditCard, amount: Double) { // case class는 new 키워드 없이 생성 가능
  def combine(other charge): Charge =
    if(cc == other.cc)
      Charge(cc, amount + other.amonut)
    else
      throw new Exception("Can't combine charges to different cards")
}
```
combine함수는 청구권을 하나로 합해지는 기능을 구현한다.

```scala
class Cafe {
  def buyCoffee(cc: CreditCard): (Coffee, Charge) = ...

  def buyCoffees(cc: CreditCard, n: Int): (List[Coffee], Charge) = {
    val purchases: List[(Coffee, Charge)] = List.fill(n)(buyCoffee(cc)) // buyCoffees n개 리스트를 생성한다
    val (coffees, charges) = purchases.unzip // 목록들 쌍으로 분리한다.
    (coffees, charges.reduce((c1, c2) => c1.combine(c2))) // 청구건들을 하나로 환원한다.
  }
}
```
buyCoffee를 직접 재사용하여 buyCoffees 함수를 정의할 수 있어었고 Payments의 모의 구현 없이 검사할수 있게 되었다.
청구건은 어떻게 처리되는지 모르고 Payments가 처리해야하지만 buyCoffee에서 알 필요가 없어졌다.

```scala
def coalesce(charges: List[Charge]): List[Charge] =
  charges.groupBy(_.cc).values.map(_.reduce(_ combine _)).toList
```
Charge를 일급값으로 만들었기 때문에 청구건들을 카드별로 취합하는 함수를 쉽게 작성이 가능해 졌다.
_ combine _ 은 익명 함수를 위한 구문

결과적으로 부수적인 효과가 발생하는 부분이 생길수 밖에 없다.
이런 함수는 관찰되지 않도록 외부에서 참조가 되지 않음을 보장할 수 있다면 변이가 가능히ㅏ고 뭔가를 기록할 수 있다.

### 1.2 (순수)함수란 구체적으로 무엇인가?
FP(functional programing)은 순수 함수들로 프로그래밍 하는것이라고 말했다.
순수 함수는 side effect가 없는 함수라며 입력으로 뭔가를 계산하는것 외에 어떤 관찰 가능한 영향도 미치지 않는다.
입력 값이 같다면 항상 같은 값을 돌려준다. 이러한 개념을 referential transparency 참조 투명성 이라는 개념을 통해 공식화할 수 있다.
참조 투명성은 함수가 아닌 expression 표현식의 한 속성이다.
표현식이란 하나의 결과로 평가되는 코드 조각이다.
2 + 3은 항상 같은 값을 꺼내고 2 + 3을 5로 모두 치환하여도 동일한 프로그램이 된다.
표현식을 평가 결과로 바꿔도 동일하고 이것을 참조에 투평한 것이라고 한다.

### 1.3 참조 투명성, 순수성, 그리고 치환 모형
```scala
class Cafe {
  def buyCoffee(cc: CreditCard, p: Payments): Coffee = {
    val cup = new Coffee()
    p.charge(cc, cup.price) // side effect 하지만 검사성은 높아졌다.
    cup
  }
}
```
순수함수라면 new Coffee()가 평가 결과기 때문에 buyCoffee(_, _)는 new Coffee()와 동일해야한다.
이부분은 거짓이기 때문에 투명하지 않다고 할수 있다.
참조 투명성은 조건이 값으로 대표된다는 불변 조건을 강제하고 이러한 제약을 지키면 substitution model 치환 모형이 가능해진다.
표현식을 전개 하고 값으로 치환해서 가장 간단한 형태로 축약하면 된다.
등치 대 등치 치환을 통해 진행이 되고ㅗ 참조 투명성은 프로그램에 대한 등식적 추론을 가능하게 한다.

```scala
val x = "hello"
val y1 = x.reverse
val y2 = x.reverse

val x = new StringBuilder("hello")
val y1 = x.append(" world")
val y2 = x.append(" world")
```
위의 코드는 참조 x를 hello로 치환하더라도 결과가 같고 참조에 투명하다고 할수 있다.
하지만 아래 코드는 x가 변형이 되기 때문에 append함수는 참조에 투명하지 않다고 할수 있다.
치환 모델은 추론이 간단하지만 그렇지 않으면 추론이 어려워진다.
모듈적인 프로그램은 component로 구성되어 구성요소의 의미와 구성요소들끼리 합성에 관한 규칙들에만 의존한다.
즉 구성요소 들끼리 합성 가능하다. 이것은 입력과 결과가 분리되어 블랙박스의 형태기 때문에 어떻게 쓰이는지 신경 쓰지 않을 수 있기 때문에 재사용할 수 있다.

### 1.4 요약
functional programing은 순수함수로만 구축하고 순수함수들은 입력과 출력의 관심사가 분리되어 합성이 편리하고 재사용성이 뛰어나다.
이러한 순수함수를 구현하기 위해서는 참조에 투명하게 만들고 치환이 가능하도록 해야한다.


## 2 스칼라로 함수형 프로그래밍 시작하기
