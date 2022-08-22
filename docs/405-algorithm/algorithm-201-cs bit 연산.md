---
layout: default
title: algorithm cs bit 연산
parent: algorithm
nav_order: 405201
---

### bit 연산자
* `&`
   * AND연산 01과 11을 비트연산 하여 01이 된다.
* `|`
   * OR연산 01과 11을 비트연산 하여 11이 된다.
* `^`
   * XOR연산 01과 11을 비트연산 하여 10이 된다.

### bit 연산 c 예제
```java
#include <stdio.h>

int main()
{
unsigned char num1 = 1;      // 0000 0001
unsigned char num2 = 3;      // 0000 0011

    printf("%d\n", num1 & num2);
    printf("%d\n", num1 | num2);
    printf("%d\n", num1 ^ num2);
 
    return 0;
}
```


### 출력
```java
1
3
2
```


### 개념
```html
8bit        = 1byte
int = 32bit = 4byte
         FF = 1byte
0xFFFFFFFF  = int

public long unsigned32(int n) {
return n & 0xFFFFFFFFL;
}
```
