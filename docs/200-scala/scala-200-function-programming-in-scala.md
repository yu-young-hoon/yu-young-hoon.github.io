---
layout: default
title: Scala 스칼라로 배우는 함수형 프로그래밍
parent: scala
nav_order: 200200
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
꼬리 재귀 함수를 이용해서 루프를 작성하는법, 고차함수, 다형적 고차함수등을 다루는 법을 알아보자.

### 2.1 스칼라 언어의 소개: 예제 하나
```scala
object MyModule { // 단일체 객체의 선언
  def abs(n: Int): Int =
    if (n < 0) -n
    else n
    
  def private def formatAbs(x: Int) = { // private는 생략해도 되지만 노출되는 함수는 반환형을 명시하자!
    val msg = "The absolute value of %d is % d"
    msg.format(x, abs(x))
  }
  
  def main(args: Array[String]): Unit = // 부수효과가 발생하는 부분 procedure 불순함수
    println(formatAbs(-42))
}
```

### 2.2 프로그램의 실행
sbt, scalac, REPL등의 방식으로 스칼라를 사용할수 있다.
* sbt: 스칼라용 빌드 TOOL
* scalac: 스칼라 컴파일러
* scala: 스칼라 해석기
* REPL: 스탈라 해석기의 대화식 모드

### 2.3 모듈, 객체, 이름공간
MyModule 객체 안에 abs 가 정의되어 있기 때문에 MyModule은 abs가 속한 이름공간이다.
스칼라의 모든 값은 객체이고 객체는 0개 또는 하나 이상의 멤버를 가질 수 있다.
자신의 멤버에게 이름 공간을 주는 목적인 객체를 모듈이라고 부른다.
2 + 1 은 2.+(1)과 동일하고 syntactic sugar(겉치레)를 제외한 infix(중위) 표기법이다.
MyModule.abs(42) 대신 MyModule abs 42를 사용해도 동일하다.
importing을 하면 abs(42) 처럼 객체 이름을 생략 할수있다. 
import MyModule.abs 또는 모든 비전용을 포함하기 위해 import MyModule._을 통해서 할수 있다.

### 2.4 고차 함수: 함수를 함수에 전달
값으로서의 함수로 다른 함수를 인수로 받는 함수를 작성하는 것이 유용한 경우가 많다.
그런 함수를 higher-order function 고차 함수, 고계 함수라고 부른다. 

#### 2.4.1 잠깐 곁가지: 함수적으로 루프 작성하기
```scala
def factorial(n: Int): Int = {
  @annotation.tailrec // 꼬리 호출 제거가 적용이 실패하면 컴파일 오류 발생 시키는 어노테이션
  def go(n: Int, acc: Int): Int = // local definition 지역정의, 내부함수로 지역 정수나 문자열과 다름없다.
    if (n <= 0) acc
    else go(n-1, n*acc)
    
  go(n, 1)
}
```
go함수는 자기 재귀를 하고있는데 재귀 호출이 꼬리 위치에서만 일어난다면 최적화를 한다.
while문과 동일하게 바이트 코드로 컴파일 하는 최적화를 꼬리 호출 제거가 적용된다.

#### 2.4.2 첫번째 고차 함수 작성
```scala
object MyModule {
  private def formatAbs(x: Int) = {
    val msg = "The absolute value of %d is %d."
    msg.format(x, abs(x))
  }
  
  private def formatFactorial(n: Int) = {
    val msg = "The factorial of %d is %d."
    msg.format(n, factorial(n))
  }
  
  def main(args: Array[String]): Unit = {
    println(formatAbs(-42))
    println(formatFactorial(7))
  }
}
```
formatAbs와 formatFactorial은 거의 동일하다 formatResult로 일반화하는 함수를 만들어 보자

```scala
// 고차 함수의 인수에는 f 처럼 짧은 이름을 사용한든 것이 관례이다.
// 인수로 들어가는 함수가 수행하는 일에 대해 구체적으로 알지 못하기 때문이다.
def formatResult(name: String, n:Int, f: Int => Int) = {  
  val msg = "The %s of %d is %d."
  msg.format(name, n, f(n))
}
```
f: Int => Int 는 int에서 int, int 화살표 int라고 읽으며 정수 하나를 받아서 정수 하나를 돌려준다는 뜻이다.
abs나 factorial도 정수 하나를 받아서 하나를 돌려주기 때문에 형식에 부합하고 f인수로 넘겨줄수 있다.

### 2.5 다형적 함수: 형식에 대한 추상
정수를 받아 정수를 내어 주는 함수는 단형적 함수이다. 즉 한 형식의 자료에만 사용하는 함수였다.
임의의 형식에 대해 작동하는 코드를 작성해야하는 경우도 많이 생긴다. 그런 함수를 다형적 함수라고 부른다.

#### 2.5.1 다형적 함수의 예
```scala
def findFirst(ss: Array[String], key: String): Int = {
  @annotation.tailrec
  def loop(n: Int): Int = 
    if (n >= ss.length) -1    // 배열을 지나치면 -1 
    else if (ss(n) == key) n  // n번째 요소가 key와 동일하다면 n
    else loop(n + 1)          // 그렇지 않다면 n을 증가
    
  loop(0)                     // 배열 첫번째 요소부터 시작
}
```
Array[String]에서 검색하던 Array[Int]에서 검색하던 코드는 거의 동일할 것이다.

```scala
def findFirst[A](as: Array[A], p: A => Boolean): Int = {
  @annotation.tailrec
  def loop(n: Int): Int = 
    if (n >= as.length) -1
    else if (p(as(n))) n
    else loop(n + 1)
    
  loop(0)
}
```
이것은 generic function 일반적 함수라고 부르는 다형적 함수의 한 예이다.
형식에 대한 추상을 적용하였고 형식 매개변수를 일반적으로 짧은 한글자 대문자로 지정한다.
형식 매개변수 목록은 형식 변수를 도입하고 함수의 본문에서 참조할수 있다.
형식 변수 A는 두곳에서 참조된다. 배열은 A타입 배열이고 함수 p는 반드시 A타입을 받아야한다.
컴파일러는 모든 findFirst에서 형식 서명과 형식 변수를 참조가 동일한 형식임을 강제한다.

#### 2.5.2 익명 함수로 고차 함수 호출
```scala
findFirst(Array(7, 9, 13), (x: Int) => x == 9)
```
익명 함수 또는 함수 리터럴을 지정해서 호출하는 것이 편한 경우가 많다.
`Array(7, 9, 13)` 은 배열 리터럴 이고
`(x: Int) => x == 9` 는 함수 리터럴 또는 익명 함수이다.
`(x: Int) => x == 9`의 경우 `(x) => x == 9` 처럼 형식 주해를 생략할 수 있다.

```scala
val lessThan = new Function2[Int, Int, Boolean] { // 스칼라 표준 라이브러리의 trait(인터페이스)
  def apply(a: Int, b: Int) = a < b
}
```
함수 리터럴인 (a, b) => a < b는 위와 같은 apply 메서드를 가진 객체의 구문적 겉치레이다.
스칼라의 함수는 보통 스칼라 객체이고 함수는 일급 값이다. 일급함수와 메서드를 둘 다 함수라고 부른다.

### 2.6 형식에서 도출된 구현
다형적 형식은 가능성 공간이 축소 되기 때문에 partial application(부분 적용)이라고 부르는 고차 함수를 사용한다.
partial 함수는 값 하나와 함수 하나를 받고 인수가 하나인 함수를 결과로 돌려준다.
partial은 이 함수가 주어진 인수들 일부에만 적용된다는 의미의 이름이다.
```scala
def partial1[A, B, C](a: A, f: (A, B) => C): B => C
```
이 함수는 인자 두개를 받는데, A와 A, B를 받고 C를 내주는 함수이다.
돌려주는 값 역시 B => C 형식의 함수이다.

```scala
def partial1[A, B, C](a: A, f: (A, B) => C): B => C =
  (b: B) => f(a, b) // 익명 함수의 본문, 추론이 가능하기 때문에 b의 타입은 생략 가능하다.
```
추가한 코드는 B형식의 값 b를 받는 함수에 돌려준다는 의미이다 이부분은 익명 함수의 본문이된다.
c는 f의 반환형이기때문에 f에 A, B를 넘겨주는 방법 밖에 없다.
방버이 한가지이기 때문에 b의 타입은 추론이 가능하고 생략이 할수 있다.

```scala
def curry[A,B,C](f: (A, B) => C): A => (B => C) =
  a => b => f(a, b)

def uncurry[A,B,C](f: A => B => C): (A, B) => C =
  (a, b) => f(a)(b)
```

```scala
def compose[A,B,C](f: B => C, g: A => B): A => C =
  a => f(g(a))
```
함수 합성의 예제이다. 표준라이브러리는 compose와 andThen을 제공한다.
`f compose g` 로 합성을 사용하면 되고 `g andThen f`와 같다

### 2.7 요약
스칼라의 기본적인 함수형 프로그래밍의 개념들이다. 
재귀를 이용한 루프, 간단한함수와 프로그램, 고차함수, 다형적 함수를 구현해보았다.

