---
layout: default
title: Javascript list(array) to map
parent: javascript
nav_order: 204110
---

간혹 list에서 map으로 변경해서 사용하게 되는 부분이 있습니다.

두개의 리스트를 비교하거나 할때 첫번째 리스트의 아이템의 키값을 두번째 리스트에서 찾아야 하기 때문에 복잡도가 n^2됩니다.

이런 상황을 피하기 위해 map으로 만들어 사용하게되면 map을 만드는데 n, 비교하는데 n, 총 2n이 되어 복잡도가 n이 되기 때문에 리스트 두개를 무작정 비교 하는것보다 훨씬 좋은 성능을 기대할수 있게 된다.

java에서는 일반적으로 stream api의 Collectors를 사용해서 합니다.

javascript에서 array를 map으로 변경하고 싶다면 아래 처럼 사용하면 됩니다.

```js
var array = [
    { keyword: '청바지', price: '100' },
    { keyword: '티셔츠', price: '98' }
];

var result = array.reduce(function(map, obj) {
map[obj.keyword] = obj;
return map;
}, {});

console.result(result);
//  {
//      청바지: {keyword: "청바지", price: "100"}
//      티셔츠: {keyword: "티셔츠", price: "98"}
//  }
```
