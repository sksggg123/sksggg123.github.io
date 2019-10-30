---
layout: customize-posts
title: Docker 정리
date: 2019-10-28
last_modified_at: 2019-10-28
description: "Docker 수업을 받고 잊지 않기 위해 정리하는 자료 입니다. 아주 기초이며 간단한 명령어 정리."
header:
    teaser: /assets/images/blog/docker/docker.png
    og_image: /assets/images/blog/docker/docker.png
keywords:
    - Docker
    - docker
    - dockerCompose
    - compose
    - image
    - build
    - dockerfile
    - Dockerfile
    - 도커파일
    - 도커
    - 이미지빌드
    - 컴포트
    - 도커허브
category:
    - Docker
tags:
    - docker
published: false
sitemap: 
    changefreq: daily
    priority: 1.0
---
<center><img src="/assets/images/blog/docker/docker.png" width="1200" height="800"></center>
> 도커에 처음 명령어를 날려보며 정리하는 글..  

## 기본 명령어
```bash
docker [명령어] [옵션]
```

|명령어|수행|
|-|-|
|run|컨테이너 실행|
|stop|컨테이너 종료|
|rm|컨테이너 삭제|
|pull|컨테이너 다운|
|rmi|이미지 삭제|
|logs|컨테이너 로그|
|exec|컨테이너 내부명령어 실행|
|network create|가상 네트워크 생성|
|network is|가상 네트워크 목록|

### **run** 명령어
```bash
> docker run --rm -d -p 7777:80 nginx
```
**--rm**과 **-d, -p** 옵션을 사용하여 **nginx** 컨테이너를 띄우는 명령어 이다.   
**--rm**의 경우 docker stop을 통해 컨테이터를 중지시킬 경우 **자동으로 컨테이너가 삭제**가 되는 옵션  
**-d**의 경우에는 컨테이너가 **백그라운드**로 수행되게 하는 옵션  
**-p**의 경우에는 **외부포트:내부포트** 명시로 앞은 host의 port이며 뒤 는 컨테이너에 접근하는 port  

위의 명령어를 통해 컨테이너를 띄우게 될 경우 local환경 기준으로 http://localhost:7777 으로 접속을 하게 되면 내부의 nginx의 80port로 포워딩이 된다.  

참고로 -d를 사용을 하게되면 nginx는 백그라운드로 수행이 되기에 접근하는 log를 바로 볼수가 없다. docker logs <Docker ID>를 통해 로그를 따로 확인을 해야한다. -d옵션을 주지 않을 경우 백그라운드에서 수행이 되지 않기에 log를 바로 출력을 해주게 된다.  

### **stop** 명령어
```bash
# nginx 컨테이너 실행
> docker run --rm -d -p 7777:80 nginx
# 실행중인 컨테이너 프로세스 확인
> docker ps -a
CONTAINER ID    IMAGE   COMMAND                  CREATED             STATUS              PORTS                  NAMES
abc7f4554813    nginx   "nginx -g 'daemon of…"   4 seconds ago       Up 3 seconds        0.0.0.0:7777->80/tcp   festive_perlman
# 실행중인 컨테이너 중지
> docker stop abc7f4554813
```

```docker ps -a```를 통해 현재 실행 or 중지된 상태의 컨테이너 목록과 상태를 확인하여 중지하고자하는 컨테이터의 ID를 확인한다. 확인 된 ID를 활용하여 컨테이너를 중지시키게 되면 STATUS의 값이 **Exited (0) 2 seconds ago**으로 상태변경이 이루어 진다. 이렇게 될 경우 단순 컨테이너가 종료된 것이지 삭제가 된 것이 아니며, ```docker start <DockerInfo>또는 docker restart <DockerInfo>```를 통해 재기동을 할 수 있다. (DockerInfo = DockerID, DockerName)


### **rm** 명령어
```bash
# 실행중인 컨테이너 프로세스 확인
> docker ps -a
CONTAINER ID    IMAGE   COMMAND                  CREATED             STATUS                     PORTS                   NAMES
abc7f4554813    nginx   "nginx -g 'daemon of…"   4 seconds ago       Up 3 seconds               0.0.0.0:7777->80/tcp    festive_perlman
cc28ffe977e     nginx   "nginx -g 'daemon of…"   3 minutes ago       Exited (128) 2 minutes ago                         angry_antonelli
> docker rm -f abc7f4554813
> docker rm cc28ffe977e
```

컨테이너 삭제 방법으로 rm을 삭용하면 된다. **-f** 옵션 없이 rm만 사용할 경우 컨테이너가 중지된 상태에서만 가능하며 중지가 안된 run 상태에서 바로 삭제하기 위해서는 **rm -f** 를 통해 삭제할 수 있다.  
