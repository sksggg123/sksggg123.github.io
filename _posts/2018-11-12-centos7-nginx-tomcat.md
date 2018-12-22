---
layout: customize-posts
title: "Centos7에 Nginx와 Tomcat 구축 및 설정하기"
category:
    - Linux
tags:
    - Centos
    - Nginx
    - Tomcat
---
# Centos 7 + Nginx + Tomcat 구축 및 설정

## Nginx 설치 및 설정
1. naginx repository 생성
    1. vi /etc/yum.repos.d/nginx.repo : 아래 내용 생성
    ``` java 
        [nginx]
        name=nginx repo
        baseurl=http://nginx.org/packages/centos/7/$basearch/
        gpgcheck=0
        enabled=1
    ```
2. Nginx 설치 명령어
    1. > yum install nginx
3. 부팅시 자동실행 설정
    1. > systemctl start nginx 
    2. > systemctl enable nginx
    3. > systemctl status nginx
4. 방화벽 설정
    1. > firewall-cmd --permanent --zone=public --add-port=80/tcp
    2. > firewall-cmd --permanent --zone=public --add-port=443/tcp
    3. > firewall-cmd -–permanent -–zone=public -–add-service=http
    4. > firewall-cmd -–permanent -–zone=public -–add-service=https
    5. > firewall-cmd --reload

2. letsencrpt 
    1. file uploading => http://eastflag.co.kr/devops-centos_nginx_springboot/
    2. 원래 SSL 인증서는 인증된 기관( CA )으로부터 발급 받아야 하는데, Let's Encrypt을 이용하면 무료로 인증서를 발급 받을 수 있습니다. 단, 90일 동안만 인증서가 유효하므로 서버에서 cron을 이용하여 주기적으로 인증서를 갱신해야 합니다.
        1. 진행 중...

## Tomcat 설치 및 설정
1. Tomcat wget
    1. > wget http://apache.mirror.cdnetworks.com/tomcat/tomcat-8/v8.5.34/bin/apache-tomcat-8.5.34.tar.gz
2. /usr/local/tomcat 디렉토리 생성
    1. > mkdir /usr/local/tomcat
    2. > mv apache-tomcat-8.5.34.tar.gz /usr/local/tomcat/apache-tomcat-8.5.34.tar.gz
    3. > tar -xvf apache-tomcat-8.5.34.tar.gz
3. 방화벽 설정
    1. > firewall-cmd --permanent --zone=public --add-port=8080/tcp
    2. > firewall-cmd --reaload
4. server.xml Encoding 추가
    1. ~/conf 디렉토리 이동
        ```java
            ## 수정 전
            <Connector port="8080" protocol="HTTP/1.1"
            connectionTimeout="20000" 
            redirectPort="8443" />

            ## 수정 후
            <Connector port="8080" protocol="HTTP/1.1"
            connectionTimeout="20000" 
            redirectPort="8443" URIEncoding="UTF-8" />
        ```

## Nginx + Tomcat 연동
1. nginx service start
    1. > service nginx start
2. tomcat service start
    1. > service tomcat8 start    
3. nginx 환경 설정
    1. > cd /etc/nginx/conf.d
    2. > vi tomcat.conf
        ```shell
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
    3. TIP) 아래와 같은 에러 로그가 있을때 조치가이드
    ``` log
        [crit] 1938#0: *4 connect() to 127.0.0.1:8080 failed (13: Permission denied) while connecting to upstream,
    ```
        
    1.  > vi /etc/selinux/config
    2.  > SELinux=enforcing -> SELinux=disabled
    3.  > 재부팅 필요

