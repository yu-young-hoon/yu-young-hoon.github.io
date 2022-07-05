---
layout: default
title: Javascript 디바운싱 스트롤링
parent: javascript
nav_order: 204105
---

## 디바운싱 스트롤링
* 스크롤이나 화면 재조정 처럼 수천번 빠르게 발생하는 이벤트 처리

```js
// 디바운싱 호출되기 전까지 시간 간격, 마지막 이벤트 부터 시간 카운트
const debounce = (func, delay) => {
    let inDebounce
    return function () {
        const context = this
        const args = arguments

        // 설정 시간 전에 이벤트 발생하면 그전 설정된 이벤트 해제
        clearTimeout(inDebounce)

        // 이벤트가 발생 안하고 시간이 됬다면 그때 이벤트 실행
        inDebounce = setTimeout(() => func.apply(context, args), delay)
    }
}
// 스트롤링 함수가 호출되기 전에 특정 시간을 기다림, 취소 없이 시간마다 이벤트 발생
const throttle = (func, limit) => {
    let inThrottle
    return function () {
        const args = arguments
        const context = this

        // 함수가 이미 시작됬다면 패스
        if (!inThrottle) {
            func.apply(context, args)
            inThrottle = true

            // 함수가 완료 되면 다시 함수 시작할수 있도록
            setTimeout(() => inThrottle = false, limit)
        }
    }
}
```