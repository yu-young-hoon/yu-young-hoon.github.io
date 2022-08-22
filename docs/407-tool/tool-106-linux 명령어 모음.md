---
layout: default
title: tool linux 명령어 모음
parent: tool
nav_order: 407106
---

==리눅스 버전확인==
grep . /etc/*-release

==port 조회==
* linux: netstat -ntlp
* mac: sudo lsof -i -n -P | grep TCP

==파일 삭제==
* rm somefile.png
* rm -i -- *  파일을 찾지 못할 경우 모든 파일을 선택하고  y/n 프롬프트에서 선택후 삭제 하는 방법도 있다.

==파일 전송==
* scp redis-5.0.7.tar.gz someuser@123.123.123.123:/home/users/someuser

==파일 찾기==
* sudo find / -name nginx.conf

==심볼릭 링크 걸기==
* ln -s  ../test/test  thetest

==서비스 확인==
systemctl list-units

==서비스 실행==
systemctl start logstash

==서비스 로그보기==
journalctl -u kibana.service -n 100 --no-pager

! 명령어 ! 설명 !
| tar -zcvf aaa.tar.gz abc                                                                | aaa.tar로 압축 |
| tar -zxvf aaa.tar                                                                       | aaa.tar 압축 해제 |
| scp host@origin:파일 경로                                                               | 원격 -> 로컬 파일 받기 |
| scp 파일 host@origin:경로                                                               | 로컬 -> 원격 파일 전송 |
| cat /etc/passwd                                                                       | 유저 목록 |
| kill -9 ``<pid>`` .                                  | 프로세스 종류 |
| ps -ef .                                        | 프로세스 확인 |
| df -h -T                                                                                | 용량보기 |
| sudo                                                                                    | root |
| service status nginx.service                                                            |       |
| amazon-linux-extras install nginx1.12 .                                                 | amazon 추가 저장소에서 설치 |
| chmod 777 test                                                                          | |
| ssh -i hassiostudio.pem ec2-user@ec2-13-209-19-118.ap-northeast-2.compute.amazonaws.com | |
| nslookup email-smtp.us-west-2.amazonaws.com                                             | dns ip 목록보기 |
| `ps -eo user,pid,ppid,rss,size,vsize,pmem,pcpu,time,cmd --sort -rss | head -n 11`       | 메모리 사용량 표시 |
| sar -r 1                                                                                | 메모리 사용량 표시(전체) |
| sudo wget https://releases.wikimedia.org/mediawiki/1.32/mediawiki-1.32.2.tar.gz         | |
| chown -R nginx:nginx chat/                                                              | 폴더 그룹, 사용자 지정 |

==참고 링크==
* [https://zetawiki.com/wiki/%EB%A6%AC%EB%88%85%EC%8A%A4_%EB%B0%98%EB%B3%B5_%EC%98%88%EC%95%BD%EC%9E%91%EC%97%85_cron,_crond,_crontab crontab]
* [http://mingu.kr/74 호스트파일수정]
