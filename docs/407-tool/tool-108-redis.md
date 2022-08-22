---
layout: default
title: tool redis
parent: tool
nav_order: 407108
---

==redis 설치==
===직접 다운로드하여 설치===
<source>
$ wget http://download.redis.io/releases/redis-5.0.7.tar.gz
$ tar xzf redis-5.0.7.tar.gz
$ cd redis-5.0.7
$ make
</source>

===apt로 설치 for ubuntu===
<source>
$ apt update
$ apt install redis-server
$ systemctl restart redis.service
</source>

==redis 비밀번호 설정==
===redis-cli로 설정===
<source>
redis 127.0.0.1:6379> auth passworld
(error) ERR Client sent AUTH, but no password is set
redis 127.0.0.1:6379> config set requirepass "mypass"
OK
redis 127.0.0.1:6379> auth mypass
Ok
</source>

===설정 파일로 설정===
* /etc/redis/redis.conf파일을 vim 또는 nano로 열기
* # requirepass foobared 부분을 찾아 주석을 제거하고 foobared를 원하는 비밀번호로 변경

==redie remote access 허용 설정==
* 기본설정은 로컬에서만 사용 가능하도록 되어있다.
* redis.conf파일을 vim 또는 nano로 열기
* bind 127.0.0.1 부분을 찾아 bind 0.0.0.0로 변경

==rdb 방식==

==aof 방식==

<source>
// 클러스터 생성
redis-cli --cluster create  \
127.0.0.1:7001 \
127.0.0.1:7002 \
127.0.0.1:7003 \
127.0.0.1:7004 \
127.0.0.1:7005 \
127.0.0.1:7006 \
--cluster-replicas 1

// 접속
redis-cli -c -p 7001
</source>


| hgetall PointContainer:1                         |     |
| flushall                               |     |
| keys *                                 |     |
| hset PointContainer:1 BONUS_PLUS 9999                        |     |

==참고링크==
* [http://wonwoo.ml/index.php/post/744 redis rdb aof 방식 차이]
* [https://www.letmecompile.com/redis-cluster-sentinel-overview/ redis 클러스, 센티넬 구성 및 동작 방식]
* [https://americanopeople.tistory.com/148 redis memcashed 차이]
* [https://meetup.toast.com/posts/224 redis toast1]
* [https://meetup.toast.com/posts/225 redis toast2]
