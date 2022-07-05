---
layout: default
title: Javascript plugin eslint
parent: javascript
nav_order: 204101
---
## eslint plugin
* https://eslint.org/

### switch-case
* eslint unexpected lexical declaration in case block 에러
* let 변수를 사용할때 중괄호 블록으로 감싸야 합니다.
* switch의 case문 하나하나가 함수라고 생각을 하면 let 키워드를 사용한 변수의 범위가 모호해지기 때문이라고 생각합니다.
* https://eslint.org/docs/rules/no-case-declarations

```js
/*eslint no-case-declarations: "error"*/
/*eslint-env es6*/

// Declarations outside switch-statements are valid
const a = 0;

switch (foo) {
// The following case clauses are wrapped into blocks using brackets
// let 변수를 사용할때 중괄호 블록으로 감싸거나 정의된 함수로 교환하거나 내부함수로 정의해야 함
    case 1: {
        let x = 1;
        break;
    }
    case 2: {
        const y = 2;
        break;
    }
    case 3: {
        function f() {
        }

        break;
    }
    case 4:
// Declarations using var without brackets are valid due to function-scope hoisting
        var z = 4;
        break;
    default: {
        class C {
        }
    }
}
```