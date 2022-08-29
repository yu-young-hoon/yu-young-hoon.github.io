---
layout: default
title: tool docker 명령어 모음
parent: tool
nav_order: 407107
---

도커 우분트 만든회사 golang koltin 경량스레드 jvm에서 스레드 생성이 비용이큼 고루틴
* Windows에서 Linux Container로 실행
* Windows에서 tool box로 설치

==docker 이미지 검색==
* 1) Docker Hub Web에 접속해 검색한다
* 2) docker search 명령어를 사용한다

==docker 이미지 받기==
* docker pull 옵션 이미지명:태그
* docker pull bde2020/hive 최신으로 받기

==docker 받은 이미지 리스트==
* docker images

==docker 이미지 삭제==
* docker rmi imageId
* -f 컨테이너와 함께 삭제

==docker file로 이미지 생성==
* docker build -f Dockerfile .

==docker 컨테이너 목록==
* docker ps
* -a Running 중이 아닌 컨테이너도 포함

==docker 컨테이너 중지/삭제==
* docker stop 854c37841b10
* docker rm 854c37841b10

==docker compose로 컨테이너 생성==
* docker-compose -f zookeeper-for-kafka.yml up
* -d 백그라운드 실행

==docker 컨테이너 접근==
* docker exec -u 0 -it jenkins bash

==docker container 속성보기==
* docker inspect  7fafa86a9919
* <source>docker inspect -f '{{ .Mounts }}' 7fafa86a9919 볼륨 상태</source> 
* <source>docker inspect -f '{{ .NetworkSettings }}' 7fafa86a9919 네트워크 상태</source>

==docker 명령어 모음==
! 명령어                                                ! 설명 !
| docker --help                                       | 명령어 일람           |
| docker login                                        | 도커 로그인           |
| docker pull jenkins                                 | 이미지 다운로드        |
| docker run                                          | 재설치, 컨테이너 생성    |
| docker run --name point-redis -d -p 6379:6379 redis |                     |
| docker exec -i -t point-redis redis-cli             |                     |

=== vim 설치 ===
* apt-get update
* apt-get install vim

=== 참고 링크 ===
* https://docs.docker.com/reference/
* https://rampart81.github.io/post/docker_commands/ 자주 쓰는 docker commands
* http://www.realhanbit.co.kr/books/226/pages/2209/preview
* https://blog.naver.com/varkiry05/221441388036 pinpoint(docker) 서버 구축 및 was(tomcat-docker) 연결
* https://www.44bits.io/ko/post/almost-perfect-development-environment-with-docker-and-docker-compose
* https://nirsa.tistory.com/81 docker compose 명령어
