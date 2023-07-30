---
layout: default
title: linux multiple ip/port are open check by shell script
parent: shell
nav_order: 206300
---

## linux에서 shell script로 ip/port open 확인을 한번에 여러개 하는법

```html
#!/bin/bash
echo "www.google.com 443
naver.com 80
192.168.0.100 1" | (
    TCP_TIMEOUT=3
    while read host port; do
        (CURPID=$BASHPID;
        (sleep $TCP_TIMEOUT;kill $CURPID) &
        bash -c 'exec 3<> /dev/tcp/'$host'/'$port';echo $?' 2>/dev/null
        ) 2>/dev/null
        case $? in
        0)
            echo $host $port is open;;
        1)
            echo $host $port is closed;;
        143|137) # killed by SIGTERM
            echo $host $port timeouted;;
        esac
    done
    ) 2>/dev/null
```
* `#!/bin/bash`를 빼고 터미널에 복붙하거나 .sh 파일로 저장하고 실행 권한을 부여해서 실행하면 된다.

```html
scanme.nmap.org 80 is closed
scanme.nmap.org 81 is closed
192.168.0.100 1 is closed
```
* 