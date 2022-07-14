---
layout: default
title: elasticsearch 에러 unable to create temporary keystore at /etc/elasticsearch/elasticsearch.keystore.tmp, write permissions required for /etc/elasticsearch or run elasticsearch-keystore upgrade
parent: error
nav_order: 102408
---

Exception in thread "main" org.elasticsearch.bootstrap.BootstrapException: org.elasticsearch.cli.UserException: unable to create temporary keystore at [/etc/elasticsearch/elasticsearch.keystore.tmp], write permissions required for [/etc/elasticsearch] or run [elasticsearch-keystore upgrade]

elasticsearch의 버전을 업그레이드 하고 나오는 에러입니다

`sudo -u elasticsearch -s /usr/share/elasticsearch/bin/elasticsearch-keystore create`
위의 명령을 실행하면 되는데 폴더의 권한이 없어서 실해되지 않습니다

`chmod g+w /etc/elasticsearch`
권한을 추가 하고 다시 실행하면 동작합니다
