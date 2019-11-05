---
layout: customize-posts
title: Docker 정리
date: 2019-10-28
last_modified_at: 2019-11-05
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
published: true
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
|network ls|가상 네트워크 목록|

## **run** 명령어
```bash
> docker run --rm -d -p 7777:80 nginx
```
**--rm**과 **-d, -p** 옵션을 사용하여 **nginx** 컨테이너를 띄우는 명령어 이다.   
**--rm**의 경우 docker stop을 통해 컨테이터를 중지시킬 경우 **자동으로 컨테이너가 삭제**가 되는 옵션  
**-d**의 경우에는 컨테이너가 **백그라운드**로 수행되게 하는 옵션  
**-p**의 경우에는 **외부포트:내부포트** 명시로 앞은 host의 port이며 뒤 는 컨테이너에 접근하는 port  

위의 명령어를 통해 컨테이너를 띄우게 될 경우 local환경 기준으로 http://localhost:7777 으로 접속을 하게 되면 내부의 nginx의 80port로 포워딩이 된다.  

참고로 -d를 사용을 하게되면 nginx는 백그라운드로 수행이 되기에 접근하는 log를 바로 볼수가 없다. docker logs <Docker ID>를 통해 로그를 따로 확인을 해야한다. -d옵션을 주지 않을 경우 백그라운드에서 수행이 되지 않기에 log를 바로 출력을 해주게 된다.  

## **stop** 명령어
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


## **rm** 명령어
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

## **pull** 명령어
```bash
> docker pull sksggg123/simple-nginx

> docker images

REPOSITORY               TAG                 IMAGE ID            CREATED             SIZE
sksggg123/simple-nginx   latest              8ab10d568e53        11 minutes ago      126MB
```

```docker pull <imageName>```을 통해 docker hub에 있는 이미지들을 다운받을 수 있다. 다운받은 뒤 ```docker images```를 통해 다운 받은 이미지 목록을 확인해보면 된다. 

## **rmi** 명령어
```bash
> docker rmi sksggg123/simple-nginx
```

```docker images```명령어를 통해 현재 다운받은 이미지들을 확인하여, 삭제하고자 하는 이미지 이름을 넣어 ```docker rmi <imageName>```을 통해 삭제할 수 있다.

## **logs** 명령어
```bash
# 백그라운드로 컨테이너 실행
> docker run --rm -d -p 7777:80 sksggg123/simple-nginx:latest

# 로그출력을 위해 컨테이너 ID 체크
> docker ps -a                                      

CONTAINER ID        IMAGE                           COMMAND                  CREATED             STATUS              PORTS                  NAMES
0fbf7e2ec72e        sksggg123/simple-nginx:latest   "nginx -g 'daemon of…"   4 seconds ago       Up 3 seconds        0.0.0.0:7777->80/tcp   elegant_swart

# 로그출력 (기본)
> docker logs 0fbf7e2ec72e
```

```docker logs <컨테이너ID>```를 통해 로그를 출력 할 수 있으며, 로그 출력 시 사용 가능한 옵션은 아래 2가지가 있다.  
1. ```docker logs -f <컨테이너ID>```의 경우 실시간으로 출력되는 log의 내용을 확인
2. ```docker logs --tail 5```의 경우 마지막의 5줄까지 적재된 로그를 출력

## **exec** 명령어
```bash
> docker exec 0fbf7e2ec72e ls
```

```docker exec <컨테이너ID> <명령어>```를 통해 **실행중인** 컨테이너에 명령어를 사용할 수 있다. exec 멸영어에 추가로 알아두어야 하는것이 2가지가 있다.  
**첫번째**로는 ```docker exec -it <컨테이너ID> bash```를 통해 실행중인 컨테이너에 접속할 수 있다.  
**두번째**로는 ```docker run -it <이미지이름> bash```와의 차이이다. ```exec```와 run의 차이로는 exec의 경우 **실행중인** 컨테이너에 접속하는 것이며 ```run```의 경우 아직 실행시키지 않은 컨테이너에 접속하는 것을 의미한다.  

> 참고!  
> ```run```을 사용했던 것은 build 된 image에 추가적인 플러그인 설치 or 고정적인 설정 변경을 하여 image의 버전을 up할 경우 사용을 했다. 아래에 정리할 image build와 commit에 대해 조금 더 다뤄볼 예정이다.

## **network** 명령어
```bash
# network 그룹 생성
> docker network create test_local

# network 그룹 확인
> docker network ls
NETWORK ID          NAME                DRIVER              SCOPE
272d96f8cd1b        test_local          bridge              local

# 컨테이너 실행 시 네트워크 그룹 명시
> docker run --rm -d -p 7777:80 --network=test_local sksggg123/simple-nginx
> docker run --rm -d -p 6666:80 --network=test_local sksggg123/simple-nginx

# 컨테이너 기본실행
> docker run --rm -d -p 8888:80 sksggg123/simple-nginx
> docker run --rm -d -p 9999:80 sksggg123/simple-nginx

# 컨테이너 리스트 확인
> docker ps -a

CONTAINER ID        IMAGE                           COMMAND                  CREATED             STATUS              PORTS                  NAMES
54c137b32b9b        sksggg123/simple-nginx          "nginx -g 'daemon of…"   3 minutes ago       Up 3 minutes        0.0.0.0:6666->80/tcp   stoic_ramanujan
803248a23ab3        sksggg123/simple-nginx          "nginx -g 'daemon of…"   5 minutes ago       Up 5 minutes        0.0.0.0:9999->80/tcp   suspicious_panini
357e3e4e1d07        sksggg123/simple-nginx          "nginx -g 'daemon of…"   6 minutes ago       Up 6 minutes        0.0.0.0:8888->80/tcp   relaxed_davinci
0fbf7e2ec72e        sksggg123/simple-nginx:latest   "nginx -g 'daemon of…"   25 hours ago        Up 25 hours         0.0.0.0:7777->80/tcp   elegant_swartz

# 컨테이너 정보 확인
> docker inspect 54c137b32b9b |grep -E "IPAddress|Hostname"
"Hostname": "54c137b32b9b"
"IPAddress": "172.18.0.3"

> docker inspect 803248a23ab3 |grep -E "IPAddress|Hostname"    
"Hostname": "803248a23ab3"
"IPAddress": "172.17.0.3"

> docker inspect 357e3e4e1d07 |grep -E "IPAddress|Hostname"  
"Hostname": "357e3e4e1d07"
"IPAddress": "172.18.0.2"

> docker inspect 0fbf7e2ec72e |grep -E "IPaddress|Hostname"
"Hostname": "0fbf7e2ec72e"
"IPAddress": "172.17.0.4"
```

```docker network create <네트워크이름>```을 통해 네트워크 그룹을 생성할 수 있다. 생성한 그룹은 ```docker network ls```를 통해 확인 할 수 있으며, 생성한 네트워크 그룹으로 컨테이트를 묶어 사용할 수 있다.  

기본적으로 컨테이터를 실행 시키게 되면 **172.17.0.0/16**으로 네트워크가 할당이 되며, 1씩 자동으로 증가가 된다. 컨테이너 마다의 격리된 네트워크(private ip, MAC) 영역을 할당받는 다는 의미이다. 그룹으로 할당을 하게 될 경우 같은 그룹군의 컨테이너끼리는 ip를 명시하지 않아도 접근이 가능하다. 

## Docker Image File Build 하기
```bash
## 현재 디렉토리 목록
> tree                                                                                   .
├── dockerfile

# 이미지 빌드하기
> docker build -t test_docker_image .

# 생성된 image 목록
> docker images
REPOSITORY               TAG                 IMAGE ID            CREATED             SIZE
test_docker_image       latest              8ab10d568e53        3 days ago          126MB
```

```docker build -t <빌드할이미지이름> <경로>```의 명령어를 통해 이미지를 빌드(생성)할 수 있다. dockerfile에 빌드할 이미지에 관련된 설정을 한 뒤 해당 명령어를 통해 빌드를 하면 된다.  
다른 경로에 있는 dockerfile을 읽을 경우에는 옵션을 바꿔주어야 한다. ```docker build -f <빌드할이미지이름> <dockerfile경로>```