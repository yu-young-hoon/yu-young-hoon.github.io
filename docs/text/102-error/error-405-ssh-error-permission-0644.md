---
layout: default
title: ssh 에러 Permissions 0644 for 'xxxxx.pem' are too open.
parent: error
nav_order: 102405
---

### Permissions 0644 for 'xxxxxx.pem' are too open.
* aws ssh -i 옵션을 통해서 접속을 시도할 때 pem 파일의 권한이 '400'이 아닐때 발생
* sudo chmod 400 xxxxx.pem 명령어를 통해 권한수정
