---
layout: default
title: Spring Error Invalid bean definition with name 'errorPageFilter'
parent: error
nav_order: 102200
---

Spring boot 2.1 부터는 Bean Overriding이 불가능 하게 되면서

```html
spring:
   main: 
     allow-bean-definition-overriding: true
```
application.yml에 추가를 해주면 된다.
