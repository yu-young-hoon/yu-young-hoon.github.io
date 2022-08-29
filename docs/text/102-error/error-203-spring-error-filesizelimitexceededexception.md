---
layout: default
title: Spring Error FileSizeLimitExceededException: The field file exceeds its maximum permitted size of 1048576 bytes
parent: error
nav_order: 102203
---

org.apache.tomcat.util.http.fileupload.impl.FileSizeLimitExceededException: The field file exceeds its maximum permitted size of 1048576 bytes.

## 이슈
spring version 을 1.5.X에서 2.3.X으로 올리면서 spring.http.multipart.max-file-size 설정이 spring.servlet.multipart.max-file-size로 변경되면서 max file size 설정이 되지 않았다.

## 원인
Spring Boot 1.3.x and earlier
* multipart.maxFileSize
* multipart.maxRequestSize
  Spring Boot 1.4.x and 1.5.x
* spring.http.multipart.maxFileSize
* spring.http.multipart.maxRequestSize
  Spring Boot 2.x
* spring.servlet.multipart.maxFileSize
* spring.servlet.multipart.maxRequestSize

버전별 다른 설정 이름

## 해결
application.yml 수정 처리
```html
spring:
  servlet:
    multipart:
      max-file-size: 10MB

```
