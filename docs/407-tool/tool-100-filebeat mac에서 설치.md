---
layout: default
title: filebeat mac에서 설치
parent: tool
nav_order: 407100
---

filebeat는 파일을 읽어 전송하는 경량화된 로그 수집기입니다.

==설치==
[[File:filebeat-01.png]]

mac에서는 간단희 brew install filebeat로 설치할수 있습니다.

==설정==
[[File:filebeat-02.png]]

설정 파일인 filebeat.yml은 /usr/local/etc/filebeat에 위치합니다.

직접 실행할따는 filebeat.yml 권한을 root로 변경해야합니다. (sudo chown root filebeat.yml)

==실행==
서비스로 실행할때는 brew service start filebeat로 실행합니다.

직접 실행할때는 sudo /usr/local/Cellar/filebeat/7.9.2/bin/filebeat -e으로 출력 모드로 실행할수 있습니다.

또는 sudo filebeat -e -d "*"으로 디버깅 모드까지 출력할수 있습니다.

==초기화==
filebeat는 자체적으로 파일을 읽는 위치를 기록하는데 초기화를 해서 다시 읽도록 할수 있다.

mv /usr/local/var/lib/filebeat/registry /usr/local/var/lib/filebeat/registry.old2
