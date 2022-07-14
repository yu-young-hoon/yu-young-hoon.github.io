---
layout: default
title: Vertica Error too complex to analyze
parent: error
nav_order: 102304
---

* The first limit is based on the stack available to the expression. Vertica requires at least 100kb of free stack. If this limit is exceeded then the error "The query contains an expression that is too complex to analyze" may be thrown. Adding additional physical memory and/or increasing the value of ulimit -s max increase the available stack and prevent the error.
* The second limit is the number of recursions possible in an analytic expression. The limit is 2000. If this limit is exceeded then the error "The query contains an expression that is too complex to analyze" may be thrown. This limit cannot be increased.

100kb의 스택과 2000의 재귀 구문 제한이 있다. 변경할수 없는 값이기 때문에 쿼리를 변경해야한다.

### 참고링크
* https://vertica.com/docs/9.2.x/HTML/Content/Authoring/SQLReferenceManual/LanguageElements/Expressions/Expressions.htm
