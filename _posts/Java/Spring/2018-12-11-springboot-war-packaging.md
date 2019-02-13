---
layout: customize-posts
title: 스프링부트에서 WAR File 생성하여 배포하기
date: 2018-12-11
last_modified_at: 2019-02-13
description: "springboot (Gradle) 에서 war packaging 하여 nginx, tomcat 서버에 애플리케이션 띄우기"
keywords:
    - springboot
    - war
    - jar
    - build
    - gradle
category:
    - Springboot
tags:
    - springboot
published: true
sitemap: 
    changefreq: daily
    priority: 1.0
---

스프링부트에서는 jar 파일을 기본적으로 생성해준다.  
참고로 나는 외부의 서버 (집에 구축한 개인웹서버 [Nginx + Tomcat + Mysql](http://sksggg123.github.io/server/centos7-nginx-tomcat/) )에 스프링 부트 프로젝트를 올릴 예정이다.  

gradle.task의 build > jar를 수행할 경우 프고젝트의 build > libs 하위 디렉토리에 *.jar 파일이 생성된다.  
생성된 jar 파일을 외부서버에 FTP로 올려 아래의 명령어를 수행해 보았다
```nginx
java -jar *.jar
```

뭔가 정상적으로 수행이 된 것으로 보이는데... 접속정보를 어떻게 가야될지 모르겠다...  
(추후에 jar로 배포하는 것을 정리할 예정이다.)  
나는 기존에 구축한 서버에 war로 배포하여 사용해왔기에 war로 패키징 하는 방법을 찾아 보았다.  
이는 하단에 build.gradle 파일과 application.java에 추가사항을 넣어 주면 gradle.task에 war로 생성할 수 있게 항목이 노출된다.

>TIP)  
>아래의 소스를 추가 후 gradle.refresh 및 빌드를 한 후에 IDE프로그램을 재부팅을 해줘야 노출됨.  
>재부팅이 답임 생기지 않으면 재부팅을 한번 해보길 권장한다.

## build.grade 추가 사항

```yaml
apply plugin: 'war'
war {
    baseName = 'projectName'    
}

dependencies {
..
providedRuntime('org.springframework.boot:spring-boot-starter-tomcat')
..
}
```
## Application java class file 추가 사항  
**SpringBootServletInitializer** 를 extents 받아야  
**SpringApplicationBuilder** **configure**(**SpringApplicationBuilder application**)를 사용할 수 가 있다.
```java
@EnableJpaAuditing
@SpringBootApplication
public class DevContentsApplication extends SpringBootServletInitializer {
    
    @Override
    protected SpringApplicationBuilder configure(SpringApplicationBuilder application) {
        return application.sources(DevContentsApplication.class);
    }

    public static void main(String[] args) {
        SpringApplication.run(DevContentsApplication.class, args);
        System.out.println("=======Server Started=======");
    }
}
```

STS 기준 프로젝트 Gradle.task의 bootwar를 수행하면 build > libs 하위에 war파일이 생성 된 것을 확인 할 수 있다.  
생성된 war를 외부 tomcat webapps 밑에 넣어두면 끝..  

