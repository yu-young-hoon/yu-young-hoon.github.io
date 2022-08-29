---
layout: default
title: jackson 에러 no Creators, like default construct, exist
parent: error
nav_order: 102403
---

자바에서 생성자가 없다면 기본 생성자를 만들어 주지만 다른 생성자가 생겼을때 기본 생성자가 없기 때문에 나오는 문제

arguments가 없는 생성자를 직접 만들어 주거나 @NoArgsConstructor를 추가하여 기본 생성자를 만들어준다.