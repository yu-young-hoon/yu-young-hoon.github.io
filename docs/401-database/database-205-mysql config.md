---
layout: default
title: database mysql config
parent: database
nav_order: 401205
---
| Command                                                                   | Notes                                |
|---------------------------------------------------------------------------|--------------------------------------|
| show variables like 'general%'                                            |show options|
| set global general_log=on;                                                | enable log|
| SET GLOBAL sql_mode=(SELECT REPLACE(@@sql_mode,'ONLY_FULL_GROUP_BY','')); | group by full만 허용하도록 하는 옵션 해제|
| SET SQL_SAFE_UPDATES = 0;                                                 | where 조건 없이 업데이트|
| group_concat_max_len                                                      | concat 글자수|

```yml
## mycnf
[mysql]
user=root
password=''
connect-expired-password

[mysqld]
general_log=1
sql_mode=""
lower_case_table_names = 1
interactive_timeout = 300
wait_timeout = 300
```