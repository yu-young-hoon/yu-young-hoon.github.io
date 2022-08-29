---
layout: default
title: Javascript 프로토 타입
parent: javascript
nav_order: 204107
---

## 프로토 타입
* Prototype.Link
* Prototype.Object 함수의 일반객체, constructor는 함수 가르킴, Prototype.Object의 __proto__는 최상위인 Object
* 모든 객체의 조상은 함수, 함수를 new로 객체 생성
* 생성된 객체의 __proto__ 조상의 Prototype.Object를 가리킴
* 조상의 Prototype.Object와 같은 변수를 출력 하려고 하면 본인에게 없는 값은 조상의 Prototype.Object의 값이 나옴