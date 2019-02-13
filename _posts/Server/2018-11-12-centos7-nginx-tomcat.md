---
layout: customize-posts
title: "Centos7에 Nginx와 Tomcat 구축 및 설정하기"
date: 2018-11-12
last_modified_at: 2019-02-13
description: "VMware에 Nginx설치 및 설정하기"
keywords:
    - vm
    - vmware
    - nginx
    - centos
    - tomcat
    - install
    - 설치
    - 설정
category:
    - Server
tags:
    - centos
    - nginx
    - tomcat
published: true
sitemap:
    changefreq: daily
    priority: 1.0
---

## Nginx 설치 및 설정

### naginx repository 생성

vi /etc/yum.repos.d/nginx.repo : 아래 내용 생성
```nginx
[nginx]
name=nginx repo
baseurl=http://nginx.org/packages/centos/7/$basearch/
gpgcheck=0
enabled=1
```

Nginx 설치 명령어  
```nginx
yum install nginx
```

부팅시 자동실행 설정
```nginx
systemctl start nginx  
systemctl enable nginx  
systemctl status nginx  
```

방화벽 설정
```nginx
firewall-cmd --permanent --zone=public --add-port=80/tcp
firewall-cmd --permanent --zone=public --add-port=443/tcp
firewall-cmd -–permanent -–zone=public -–add-service=http
firewall-cmd -–permanent -–zone=public -–add-service=https
firewall-cmd --reload
```

letsencrpt  
    1. file uploading => http://eastflag.co.kr/devops-centos_nginx_springboot/  
    2. 원래 SSL 인증서는 인증된 기관( CA )으로부터 발급 받아야 하는데, Let's Encrypt을 이용하면 무료로 인증서를 발급 받을 수 있습니다. 단, 90일 동안만 인증서가 유효하므로 서버에서 cron을 이용하여 주기적으로 인증서를 갱신해야 합니다.

## Tomcat 설치 및 설정
### Tomcat wget

```nginx
get http://apache.mirror.cdnetworks.com/tomcat/tomcat-8/v8.5.34/bin/apache-tomcat-8.5.34.tar.gz
```

### /usr/local/tomcat 디렉토리 생성

```nginx
mkdir /usr/local/tomcat
mv apache-tomcat-8.5.34.tar.gz /usr/local/tomcat/apache-tomcat-8.5.34.tar.gz
tar -xvf apache-tomcat-8.5.34.tar.gz
```

### 방화벽 설정

```nginx
firewall-cmd --permanent --zone=public --add-port=8080/tcp
firewall-cmd --reaload
```

### server.xml Encoding 추가
~/conf 디렉토리 이동
```xml
<!-- 수정 전 -->
<Connector port="8080" protocol="HTTP/1.1"
connectionTimeout="20000" 
redirectPort="8443" />

<!-- 수정 후 -->
<Connector port="8080" protocol="HTTP/1.1"
connectionTimeout="20000" 
redirectPort="8443" URIEncoding="UTF-8" />
```

## Nginx + Tomcat 연동

### nginx service start
```nginx
service nginx start
```

### tomcat service start
```nginx
service tomcat8 start    
```

### nginx 환경 설정
```nginx
cd /etc/nginx/conf.d
vi tomcat.conf

    # 편집모드
    upstream tomcat {
            ip_hash;
            server 127.0.0.1:8080;
    }

    server {
        listen       80;
        server_name  localhost;

        #charset koi8-r;
        access_log  /var/log/nginx/sksggg123.access.log;

        location / {
        proxy_set_header	Host $http_host;
        proxy_set_header	X-Real-IP $remote_addr;
        proxy_set_header	X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header	X-Forwarded-Proto $scheme;

        proxy_pass http://tomcat;
        proxy_redirect	off;
        charset utf-8;
        }

    }
```
TIP) 아래와 같은 에러 로그가 있을때 조치가이드
```nginx
# 문제로그
[crit] 1938#0: *4 connect() to 127.0.0.1:8080 failed (13: Permission denied) while connecting to upstream,

# 해결방법
vi /etc/selinux/config
SELinux=enforcing -> SELinux=disabled
재부팅 필요
```