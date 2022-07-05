---
layout: default
title: Javascript front framwork vue.js 정리
parent: javascript
nav_order: 204108
---

### nodejs 설치
https://nodejs.org/ko/

### vue
* vue-cli 설치
  ** $ npm install --g vue-cli
* vue 패키지 생성
  ** $ vue init webpack vue
* vue/config/index.js 빌드파일 위치 설정
```js
 build: {
    // Template for index.html
    index: path.resolve(__dirname, '../../src/main/resources/static/index.html'),

    // Paths
    assetsRoot: path.resolve(__dirname, '../../src/main/resources/static'),
    assetsSubDirectory: 'static',
    assetsPublicPath: '/',
    
    //'''
}
```

### spring
* application.properties front폴더 위치 설정
```js
spring.thymeleaf.prefix=classpath:/static/
```

### 참고링크
* vue document https://kr.vuejs.org/v2/guide/index.html
* Vue express 이용한 개발 환경 구성 http://vuejs.kr/2017/02/05/express-with-vue/
* Vue.js 개발을 위한 주요 ES6 문법 4가지 https://joshua1988.github.io/web-development/translation/essential-es6-features-for-vuejs/
* Vue.js 스프링 연동 https://febdy.tistory.com/65
* vue 컴포넌트 테스트 https://tech.kakao.com/2019/11/27/kakao-business-vue-component-test/
