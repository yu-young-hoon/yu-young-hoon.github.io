---
layout: default
title: Javascript this 키워드
parent: javascript
nav_order: 204103
---

## this
* 함수에서 this : window
* use strict : undefined
* 내부함수 : 객체

```js
var numbers = {
   numberA: 5,
   numberB: 10,
   sum: function() { // 내부함수
     console.log(this === numbers); // => true
     function calculate() { // 내부함수 아님
       // this는 window, 엄격 모드였으면 undefined
       console.log(this === numbers); // => false
       return this.numberA + this.numberB;
     }
     return calculate(); // calculate.call(this);로 하면 정상 동작, 문맥을 바꿔줌
   }
};
numbers.sum(); // NaN, 엄격 모드였으면 TypeError
```
