---
layout: default
title: cpp 연산자 오버로딩
parent: cpp
nav_order: 207101
---

* cpp 연산자 오버로딩 기본 사용법과 for문에서 후위 연산자(i++)보다 전위 연산자(++i)를 사용하는 이유를 알아보자.

```cpp
#include <iostream>

using namespace std;

class Integer
{
private:
int value = 0;
public:
// 전위 연산자
Integer& operator++()
{
value = value + 1;
return *this;
}

	// 후위 연산자
	Integer& operator++(int)
	{
		Integer temp;
		temp = value;
		value = value + 1;
		return temp;
	}

	Integer& operator+(const int newValue) {
		value = value + newValue;
		return *this;
	}

	Integer& operator=(const int newValue) {
		value = newValue;
		return *this;
	}

	void printValue()
	{
		cout << value << endl;
	}
};

void main() {
Integer integer;

	integer = ++integer;
	integer.printValue();

	integer = integer++;
	integer.printValue();

	integer = integer + 4;
	integer.printValue();

	integer = integer.operator+(5);
	integer.printValue();

	integer = 0;
	integer.printValue();
}
```

```
출력
1
1
5
10
0
```

* 연산자 오버로딩(operator overloading)을 할때 오버로딩 하게되는 연산자는 보통 4가지이다.
    * `= (할당 연산자, assignment operator)`
    * `+ - * (이진 산술 연산자, binary arithmetic operators)`
    * `+= -= *= (복합 할당 연산자, compound assignment operators)`
    * `== != (비교 연산자, comparison operators)`

* Integer라는 box 타입의 클래스를 만들게 되면 할당, 산술, 증감 연산자를 만들게 될텐데 몇가지만 형태를 보면 아래와 같다.
    * Integer& operator++() 형태의 전위 연산자
    * Integer& operator++(int) 형태의 후위 연산자
    * Integer& operator+(const int newValue) 형태의 산술 연산자
    * Integer& operator=(const int newValue) 형태의 할당 연산자

* Integer& operator++(int) 형태의 후위 연산자를 보게 되면 temp를 생성하여 되돌려준 후에 값을 더하게된다.
* 그렇기 때문에 1이 더해지기 전인 값이 나오게 된다. temp를 생성하는 비용도 들게 된다.
* 그렇기 때문에 같은 작업을 for문의 인자로 사용하게 된다면 후위 연산자인 i++ 보다 전위 연산자인 ++i사용을 지향한다.
* 물론 최적화 되기 때문에 i++을 사용하여도 문제는 없다.

## 오버로딩 불가능한 연산자
`. .* :: ?: sizeof`

## 참고 링크
* https://edykim.com/ko/post/c-operator-overloading-guidelines/ C++ 연산자 오버로딩 가이드라인
