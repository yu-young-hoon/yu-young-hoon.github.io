---
layout: default
title: Javascript event.target와 event.currentTarget 차이
parent: javascript
nav_order: 204100
---

* event.target은 이벤트 버블링 최말단 요소 반환: 클릭된 요소를 기준으로 사용하는 경우 사용
* event.currentTarget의 경우 이벤트가 바인딩된 요소 반환

```js
<div onclick="checkTarget();">
    <span>test</span>
</div>

function checkTarget(event) {
    console.log(event.target);
    console.log(event.currentTarget은);
}
```
* span을 클릭 했을때 target은 span을 currentTarget은 div를 출력 한다.