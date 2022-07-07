---
layout: default
title: Javascript 즉시실행함수 표현식
parent: javascript
nav_order: 204111
---

```js
// 기본적인 즉시실행함수 표현식
(function () {

})();

// JavaScript 엔진의 parser는 function 키워드가 처음으로 나오면 함수 선언문으로 인식하기 때문에 동작하지 않는다
function () {

}();

// JavaScript parser에서 이런 모습의 코드를 동작시키기 위해 `!`문자를 보고 함수 선언이 아닌 표현으로 인식하게 하는 방법
!function () {

}();

// 또다른 방법들
+function () {

}();
-function () {

}();
~function () {

}();
```

### 참고링크
* https://ultimatecourses.com/blog/what-function-window-document-undefined-iife-really-means
