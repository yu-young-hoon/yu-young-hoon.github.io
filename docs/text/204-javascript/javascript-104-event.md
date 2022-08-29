---
layout: default
title: Javascript 이벤트 방식, 메소드
parent: javascript
nav_order: 204104
---

## 이벤트 방식, 메소드

```js
// 기본
for (let item of items) {
      item.addEventListener('click', function() {
        alert('you clicked on item: ' + item.innerHTML);
      });
}
// 위임방식
app.addEventListener('click', function(e) {
      if (e.target && e.target.nodeName === 'LI') {
        let item = e.target;
        alert('you clicked on item: ' + item.innerHTML);
      }
});
```
