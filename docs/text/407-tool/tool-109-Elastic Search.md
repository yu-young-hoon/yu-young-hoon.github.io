---
layout: default
title: tool Elastic Search
parent: tool
nav_order: 407109
---

==ELK==
Elastic search, logstash, kibana를 묶어서 사용하는 경우를 말합니다

==ELK Docker로 세팅==
* git clone https://github.com/deviantony/docker-elk.git
* cd docker-elk
* docker-compose up -d

==elasticsearch health 체크==
* curl -XGET http://localhost:9200/_cluster/health?pretty=true
* curl -XGET https://localhost:9200/_cluster/health?pretty=true
* curl -u elastic:elastic -XGET http://localhost:9200/_cluster/health?pretty=true

==참고링크==
* [https://osc131.tistory.com/104 elk 개요]
* [https://khanrc.tistory.com/entry/검색엔진-라이브러리 lucene solr elasticsearch 차이]
* https://coding-start.tistory.com/187 ELK Stack - Filebeat(파일비트)란? 간단한 사용법
* https://raye.dev/setup-elk-0 elk docker 설치
