---
layout: default
title: cpp11
parent: cpp
nav_order: 207102
---

## 모던 CPP
* rvalue ref : 생성되자 마자 사라지는 값을 오른쪽 값이라 함, 오른쪽값을 참조.a i++은 오른쪽값.
```cpp
int nValue;
int& lref1 = nValue;     // nValue 왼쪽 값이므로 문제 없음
int& lref2 = 10;         // 오류, 10은 오른쪽 값

int&& rref1 = 10;        // 10은 오른쪽 값이므로 문제 없음
int&& rref2 = nValue;    // 오류, nValue가 왼쪽값
```
* Number(Number&& rhs) : 이동 생성자, rvalue와 함께 추가, 카피 생성자보다 빠름
* Number(Number& rhs)  : 카피 생성자
* emplace_back을 사용하면 컨테이너에서 객체가 바로생성 카피도 안일어남
* push_back의 경우 생성 이동 소멸 소멸을 거침, 이동생성자를 만들지 않았다면 카피 생성자
* 클래스 멤버 변수 초기화 
* auto 컴파일때 타입 자동 결정, iterator 사용시에 유용
* 람다 auto func = []{}; func();
* range base for : for(auto I : list)
* nullptr, std::array<int, 5> 등 포인터 자료구조
* chrono 나노세컨드까지 초정밀 타임 객체
* 뮤택스, 락가드

```cpp
#include <mutex>
#include <thread>

std::mutex g_i_mutex;

std::lock_guard<std::mutex> lock(g_i_mutex);
std::thread t1(safe_increment);
t1.join();
```
