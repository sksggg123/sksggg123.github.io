---
layout: customize-posts
title: "Centos7에 Mysql 설정 및 연동"
date: 2018-11-12
last_modified_at: 2019-02-13
description: "VMware에 Centos 설치 후 Mysql 5.7.20 설치 및 설정(기본설정 및 포트 오픈)"
keywords:
    - vm
    - vmware
    - nginx
    - centos
    - tomcat
    - install
    - 설치
    - 설정
    - mysql
    - db
    - port
    - firewall
    - 방화벽
    - 포트
    - 오픈
category:
    - Server
tags:
    - centos
    - mysql
published: true
sitemap:
    changefreq: daily
    priority: 1.0
---
## Centos7 Mysql 5.7.20 설치

설치할 버전을 찾기 위해  
MySQL홈페이지 - DOWNLOADS - Community - MySQL Yum Repository  
아래 A Quick Guide to Using the MySQL Yum Repository 링크를 클릭한다. [Click! (go to download page)](https://dev.mysql.com/doc/mysql-yum-repo-quick-guide/en/)

Page 중간 부분에 "Within the MySQL Yum repository (https://repo.mysql.com/yum/)" 찾아서 이동. [Click! (go to download page)](https://repo.mysql.com/yum/) 링크 이동

5.7.20 버전을 받기 위해 "mysql-5.7-community/el/7/x86_64/" 으로 이동 (원하시는 버전 이동하여 설치하시기 바랍니다.)
>밑의 4가지 설치 할 예정  
>mysql-community-common-5.7.20-1.el7.x86_64.rpm  
>mysql-community-libs-5.7.20-1.el7.x86_64.rpm  
>mysql-community-client-5.7.20-1.el7.x86_64.rpm  
>mysql-community-server-5.7.20-1.el7.x86_64.rpm  

위의 4가지 wget 을 통해 설치 (순서대로 - Server, client 설치 시 common과 libs가 설치 되어있어야 하기때문에...)
```nginx
wget http://repo.mysql.com/yum/mysql-5.7-community/el/7/x86_64/mysql-community-common-5.7.20-1.el7.x86_64.rpm
    rpm -ivh mysql-community-common-5.7.20-1.el7.x86_64.rpm

wget http://repo.mysql.com/yum/mysql-5.7-community/el/7/x86_64/mysql-community-libs-5.7.20-1.el7.x86_64.rpm
     rpm -ivh mysql-community-libs-5.7.20-1.el7.x86_64.rpm

wget http://repo.mysql.com/yum/mysql-5.7-community/el/7/x86_64/mysql-community-client-5.7.20-1.el7.x86_64.rpm
    rpm -ivh mysql-community-client-5.7.20-1.el7.x86_64.rpm

wget http://repo.mysql.com/yum/mysql-5.7-community/el/7/x86_64/mysql-community-server-5.7.20-1.el7.x86_64.rpm
    rpm -ivh mysql-community-server-5.7.20-1.el7.x86_64.rpm
```

TIP) ```rpm -ivh mysql-community-server-5.7.20-1.el7.x86_64.rpm``` 설치 시 아래와 같은 error 발생 시 조치방법
```nginx
error : 오류: Failed dependencies:net-tools is needed by mysql-community-server-5.7.20-1.el7.x86_64

1. yum install http://repo.mysql.com/yum/mysql-5.7-community/el/7/x86_64/mysql-community-server-5.7.20-1.el7.x86_64.rpm

2. rpm -ivh mysql-community-server-5.7.20-1.el7.x86_64.rpm
```

TIP) 혹시 설치 관련해서 문제가 발생하여 삭제를 원할 경우..
```nginx
yum remove mysql mysql-server
rm -f -r /var/lib/mysql
```   

설치가 완료되었다. 실행되는지 확인해 보자

명령어 입력
```nginx 
sudo service mysqld start
```  

정상 start 여부 확인 
```nginx
sudo service mysqld status
```

```nginx
[root@sksggg123 /]# sudo service mysqld status
Redirecting to /bin/systemctl status mysqld.service
● mysqld.service - MySQL Server
Loaded: loaded (/usr/lib/systemd/system/mysqld.service; enabled; vendor preset: disabled)
Active: active (running) since 화 2018-11-06 09:23:11 KST; 3min 37s ago
    Docs: man:mysqld(8)
        http://dev.mysql.com/doc/refman/en/using-systemd.html
Process: 6900 ExecStart=/usr/sbin/mysqld --daemonize --pid-file=/var/run/mysqld/mysqld.pid $MYSQLD_OPTS (code=exited, status=0/SUCCESS)
Process: 6824 ExecStartPre=/usr/bin/mysqld_pre_systemd (code=exited, status=0/SUCCESS)
Main PID: 6903 (mysqld)
CGroup: /system.slice/mysqld.service
        └─6903 /usr/sbin/mysqld --daemonize --pid-file=/var/run/mysqld/mysqld.pid

11월 06 09:23:06 sksggg123 systemd[1]: Starting MySQL Server...
11월 06 09:23:11 sksggg123 systemd[1]: Started MySQL Server.
```

mysql 기본설정
```nginx
vi /etc/my.cnf

[client]
default-character-set = utf8

[mysqld]
validate_password_policy=LOW <- password 규칙을 낮추자

character-set-client-handshake=FALSE
init_connect="SET collation_connection = utf8_general_ci"
init_connect="SET NAMES utf8"
character-set-server = utf8
collation-server = utf8_general_ci

default-character-set = utf8

[mysqldump]
default-character-set = utf8

[mysql]
default-character-set = utf8
```
재기동 
```nginx
systemctl restart mysqld
```

mysql 사용자 관리 및 DB 생성

초기 password는 임시 비밀번호다 아래 명령어로 비밀번호 확인하자.
```nginx
    [root@sksggg123 /]# grep 'temporary password' /var/log/mysqld.log
    2018-11-06T00:23:07.608378Z 1 [Note] A temporary password is generated for root@localhost: *ah8l#c+ogSf
```

mysql login

Enter password -위의 임시비밀번호 입력
```nginx
[root@sksggg123 etc]# mysql -u root -p mysql
Enter password:
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 5
Server version: 5.7.20

Copyright (c) 2000, 2017, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.
```    

root password reset
```nginx
mysqlALTER USER 'root'@'localhost' IDENTIFIED BY 'new password';
mysqlFLUSH PRIVILEGES;
```
```nginx
TIP) 6번의 my.cnf 에서 validate_password_policy=LOW 설정값을 넣지 않을 경우 default 규칙은 아래와 같다

기본 8자이상, 숫자, 소문자, 대문자, 특수문자 포함
```

password reset 후 쿼리 수행되는지 확인해보기
```sql
mysqlselect 1;
+---+
| 1 |
+---+
| 1 |
+---+
1 row in set (0.00 sec)
```        

quit로 mysql 빠져 나간 뒤 변경한 password로 로그인이 되는지 확인하면 마무리~


방화벽 port open

sudo firewall-cmd --list-ports 명령어를 통해 현재 방화벽 상태 확인  
현재 웹서버를 설치 해둔 상태이기에 80, 443, 8080 port가 열린 상태이다.  
```nginx
[root@sksggg123 etc]# sudo firewall-cmd --list-ports
80/tcp 443/tcp 8080/tcp
```

sudo firewall-cmd --zone=public --add-port=3306/tcp --permanent 명렁어를 통해 3306 port open    
```nginx
[root@sksggg123 etc]# sudo firewall-cmd --zone=public --add-port=3306/tcp --permanent
success
[root@sksggg123 etc]# sudo firewall-cmd --reload
success
[root@sksggg123 etc]# sudo firewall-cmd --list-ports
80/tcp 443/tcp 8080/tcp 3306/tcp
```

외부 Tool을 통해 DB에 바로 접속 하기 위해서는 아래 설정이 필요하다  
모든 IP 허용
```nginx
mysqlGRANT ALL PRIVILEGES ON *.* TO root@'%' IDENTIFIED BY 'password';
Query OK, 0 rows affected, 1 warning (0.00 sec)

mysqlFLUSH PRIVILEGES;
Query OK, 0 rows affected (0.00 sec)
```

특정 대역 허용
```nginx
mysqlGRANT ALL PRIVILEGES ON *.* TO root@'xxx.xxx.%' IDENTIFIED BY 'password';
Query OK, 0 rows affected, 1 warning (0.00 sec)

mysqlFLUSH PRIVILEGES;
Query OK, 0 rows affected (0.00 sec)
```

특정 IP 허용
```nginx
mysqlGRANT ALL PRIVILEGES ON *.* TO root@'xxx.xxx.xxx.xxx' IDENTIFIED BY 'password';
Query OK, 0 rows affected, 1 warning (0.00 sec)

mysqlFLUSH PRIVILEGES;
Query OK, 0 rows affected (0.00 sec)
```



참고 사이트 : http://myjamong.tistory.com/6?category=833422

