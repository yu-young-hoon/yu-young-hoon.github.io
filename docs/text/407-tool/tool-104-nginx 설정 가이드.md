---
layout: default
title: tool nginx 설정 가이드
parent: tool
nav_order: 407104
---

==nginx aws에서 설치==
* sudo amazon-linux-extras install nginx1.12
* sudo service status nginx.service
* linux conf 위치: sudo vim /etc/nginx/nginx.conf

==nginx 설정 예시==
<source lang="php" line="line">
user nginx;
worker_processes auto;
error_log /home/logs/nginx-error.log;
pid /run/nginx.pid;

include /usr/share/nginx/modules/*.conf;

events {
worker_connections 1024;
}

http {
client_max_body_size 20m;
log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
'$status $body_bytes_sent "$http_referer" '
'"$http_user_agent" "$http_x_forwarded_for"';

    access_log  /home/logs/nginx-access.log  main;

    sendfile            on;
    tcp_nopush          on;
    tcp_nodelay         on;
    keepalive_timeout   65;
    types_hash_max_size 2048;

    include             /etc/nginx/mime.types;
    default_type        application/octet-stream;

    include /etc/nginx/conf.d/*.conf;

    server {
        listen       80 default_server;
        listen       [::]:80 default_server;
        return 301   http://wiki.simuruk.com;
    }

    server {
        server_name wiki.simuruk.com;
        root /home/mediawiki;
        index index.php;
        autoindex off;

        client_max_body_size 5m;
        client_body_timeout 60;

        location / {
             try_files $uri $uri/ @rewrite;
        }

        # sitemap xml 위치
        location /sitemap {
        }

        # sitemap 생성 php 실행 url
        location /sitemap-update {
            fastcgi_param SCRIPT_FILENAME $document_root/RunMakeSitemap.php;
            include fastcgi_params;
            fastcgi_pass unix:/var/run/php-fpm.sock;
        }

        # google verification
        location /google1234.html {
            return 200 'google-site-verification: google1234.html';
        }

        # naver verification
        location /naver1234.html {
            return 200 'naver-site-verification: naver1234.html';
        }

        location @rewrite {
            rewrite ^/(.*)$ /index.php?title=$1&$args;
        }

         location ^~ /maintenance/ {
             return 403;
         }

        location ~ \.php$ {
            include fastcgi_params;
            fastcgi_pass unix:/var/run/php-fpm.sock;
            fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        }

         location ~* \.(js|css|png|jpg|jpeg|gif|ico)$ {
             try_files $uri /index.php;
             expires max;
             log_not_found off;
         }

         location = /_.gif {
             expires max;
             empty_gif;
         }

         location ^~ /cache/ {
             deny all;
         }

         location /dumps {
             root /home/mediawiki/local;
             autoindex on;
         }
    }
}
</source>

==참고링크==
* [https://opentutorials.org/module/384/4526 nginx 환경설정]
