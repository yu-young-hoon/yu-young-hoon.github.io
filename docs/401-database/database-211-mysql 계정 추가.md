---
layout: default
title: database mysql 계정 추가
parent: database
nav_order: 401211
---

### mysql 계정과 host 추가, 접근권한 추가
```sql
--구버전
INSERT INTO mysql.user (host, user, password,ssl_cipher,x509_issuer,x509_subject,authentication_string) 
VALUES ('192.168.0.%', 'root', password('1234'),'','','','');

--5.5이상
INSERT INTO mysql.user (host, user, password,ssl_cipher,x509_issuer,x509_subject,authentication_string)
VALUES ('192.168.0.%', 'root', password('1234'),'','','','');

--5.7이상
insert into mysql.user(host, user, authentication_string, ssl_cipher, x509_issuer, x509_subject)
values('192.168.0.%', '계정', password('1234'), '', '', '');

--계정 host에 권한 모두 추가
GRANT ALL PRIVILEGES ON *.* TO 'root'@'192.168.0.%';

--적용
FLUSH PRIVILEGES;
```
