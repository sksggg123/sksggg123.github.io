---
layout: customize-posts
title: Springboot + Vue 연습하기 (연동)
date: 2019-04-22
last_modified_at: 2019-04-22
description: "springboot (Gradle) 에서 frontend 로는 vue로 Restful API"
keywords:
    - springboot
    - gradle
    - JPA
    - Vue
    - Restful
    - API
category:
    - Springboot
    - Vue
tags:
    - springboot
    - vue
published: false
sitemap: 
    changefreq: daily
    priority: 1.0
---


1. SpringBoot 생성 후 초기 디렉토리 구조  
![스프링부트 그래드 초기프로젝트 구조](/assets/images/blog/springBoot_Vue/springboot_gradle_init_directory.png)

2. SpringBoot 생성 후 Controller 생성  
![스프링부트 그래드 초기프로젝트 구조](/assets/images/blog/springBoot_Vue/springboot_gradle_controller.png)

-> Run하여 localhost:8080/main 테스트 해보기

3. Vue 프로젝트 추가하기
```bash
➜  boot-vue git:(master) ✗ vue init webpack-simple frontend

? Project name frontend
? Project description A Vue.js project
? Author 권병윤 <sksggg123@gmail.com>
? License MIT
? Use sass? No

   vue-cli · Generated "frontend".

   To get started:
   
     cd frontend
     npm install
     npm run dev
```

4. Vue dependencies install
``` bash
# install dependencies
npm install
```
![스프링부트 vue 접속](/assets/images/blog/springBoot_Vue/springboot_vue init.png)  

5. Vue run!
```bash
# serve with hot reload at localhost:8080
npm run dev
![스프링부트 vue 디렉토리 구조 접속](/assets/images/blog/springBoot_Vue/springboot_vue_init_directory.png)