---
layout: default
title: Javascript closure
parent: javascript
nav_order: 204102
---

## 클로저란?
* 함수와 함수가 선언된 환경의 조합
* 일급 객체함수의 개념을 이용해서 유효 범위를 묶는 바인딩
* 클로저가 만들어질때 정의됨
* getter, setter, private 함수 흉내낼수 있음

```js
// getter, setter를 흉내낸 예시
var createPet = function (name) {
    var s;
    return {
        setName: function (newName) {
            name = newName;
        },
        getName: function () {
            return name;
        },
        setS: function (newS) {
            s = newS;
        }
    }
}

// 스코프 밖의 변수에 접근이 제대로 안오게됨
for (var i = 0; i < arr.length; i++) {
    setTimeout(function () {
        console.log('The index of this number is: ' + i);
    }, 3000);
}

// 클로저 사용 반복문 즉시호출 함수 형식으로 함수 인자로 한번더 감싸서 전달
setTimeout(function (i_local) {
    return function () {
        console.log('The index of this number is: ' + i_local);
    }
}(i), 3000);

for (var i = 0; i < 5; i++) {
    (function (i) {
        setTimeout(function () {
            console.log(i);
        }, 1000);
    })(i);
}

//  let 사용, let 은 함수가 호출 될 때 마다 인덱스 i 값이 바인딩
for (let i = 0; i < arr.length; i++) { // let 블록 변수 변화되는값, const 상수값
    setTimeout(function () {
        console.log('The index of this number is: ' + i);
    }, 3000);
}
```
