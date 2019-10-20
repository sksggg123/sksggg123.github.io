---
layout: customize-posts
title: Vue 공부
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

## 프로젝트를 구성 (Spring Boot + Vue.js)

### 프로젝트 구성 (Back-end - Spring Boot)
프로젝트는 Springboot + gradle로 만들자 만들게 되면 아래와 같은 디렉토리 구조의 Back-end를 갖게 된다.  
![스프링부트 그래들 초기프로젝트 구조](/assets/images/blog/springBoot_Vue/springboot_gradle_init_directory.png)

그래도 helloworld는 봐야 제대로 프로젝트를 구성했다는 느낌이 있기에 Controller를 만들어 서버를 한번 띄워보자.  
![Controller 추가](/assets/images/blog/springBoot_Vue/springboot_gradle_controller.png)
```java
package com.sksggg123.blog.bootvue.controller;

import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class ContentListController {

    @RequestMapping(value = "/main")
    public String main() {
        return "Hello Wolrd";
    }
}
```

### 프로젝트 구성 (Front-end - Vue.js)
npm이 설치되어있다는 가정하에 아래의 command를 수행하면 vue를 위에서 만들 Back-end 프로젝트에 추가시킬수 있다.  
```bash
> vue init webpack <directoryName>
```
```log
[ 설치 Log ]
gwonbyeong-yun@gwonbyeong-yun-ui-MacBook-Pro  ~/git/dev/locker  vue init webpack frontend                                                                                                                     ✔  10015  21:11:54

? Project name frontend
? Project description A Vue.js project
? Author 권병윤 <sksggg123@gmail.com>
? Vue build standalone
? Install vue-router? Yes
? Use ESLint to lint your code? Yes
? Pick an ESLint preset Standard
? Set up unit tests Yes
? Pick a test runner jest
? Setup e2e tests with Nightwatch? Yes
? Should we run `npm install` for you after the project has been created? (recommended) npm

   vue-cli · Generated "frontend".


# Installing project dependencies ...
```

위의 명령어를 통해 현재 디렉토리에 vue프로젝트를 초기화 시키고 생성된 vue디렉토리로 진입하여 아래의 명령어를 수행한다. (나는 Vue의 프로젝트 이름을 frontend로 초기화 시킴)
```bash
> cd <directoryName>
> npm install
```
위의 명령어는 초기화한 vue 디렉토리 내부에 package.json에 정의되어있는 의존성 라이브러리를 설치하는 과정이다. 이로써 vue를 사용할 준비는 완료되었다. 아래의 명령어를 통해 vue서버를 띄워보자.
```bash
> npm run dev
```
위의 명령어를 통해 vue서버가 뜨게된다. 참고로 위의 절차대로 한번에 쭉 진행하게 될 경우 기존의 springboot서버가 8080 port를 선점하고 있기때문에 vue 서버는 8081로 띄워지게 된다. 우선 vue 화면이 정상적으로 보여지는지 http://localhost:8081 로 접속을 해보자. 보여지게 된다면 vue도 구현할 준비가 완료가 된 것이다.  

![스프링부트 vue 디렉토리 구조](/assets/images/blog/springBoot_Vue/springboot_vue_init_directory.png)

### Back-end (springboot)와 Front-end (Vue)를 연동해보자.
지금까지는 springboot는 8080, vue는 8081으로 서버를 띄워 사용하는 상태이다. 이 상태로 개발을 한다면 서버구조가 웹서버 -> 와스서버의 구조와 같은 기분이다. 하나로 합쳐서 하나의 port로 접속해보자.  

Vue의 config > index.js 파일을 열어보면 아래와 같은 형태의 소스가 있다. 소스를 아래처럼 아주살짝 수정을 해야지만 된다. 기존에 index.html을 바라보던 곳을 springboot의 index.html을 바라보게 설정을 해주면 된다. (springboot에 index.html이 없으면 만들어주면 된다.)
```java
// index: path.resolve(__dirname, '../dist/index.html'),
index: path.resolve(__dirname, '../../src/main/resources/static/index.html'),

// Paths
// assetsRoot: path.resolve(__dirname, '../dist'),
assetsRoot: path.resolve(__dirname, '../../src/main/resources/static'),
```
위와 같이 설정을 하고 springboot를 재실행 시켜도 적용이 되진 않는다. 필히 vue프로젝트를 build를 한번 수행시켜야지 된다. 아래 명령어를 통해 vue를 build해보자.
```bash
> cd frontend
> npm run build
```
build가 끝났으면 springboot의 indext.html 파일로 가보면 한줄로 소스코드가 생긴것을 확인할 수 있다. 이제 Re Run을 통해 Springboot를 재실행 해보자. 그리고 http://localhost:8080 으로 접속하여 아래의 Vue화면을 보게된다면 연동까지 마무리 된거다. 

![스프링부트 vue 접속](/assets/images/blog/springBoot_Vue/springboot_vue_init.png)

### 반응형, Favicon 설정 (기종, 브라우저 등.. 최적화)
[여기](https://developers.google.com/web/tools/lighthouse/audits/has-viewport-meta-tag?hl=ko)를 눌러 들어가보면 중간쯤에 아래와 같은 소스가 있다.
```html
<head>
  ...
  <meta name="viewport" content="width=device-width, initial-scale=1"> <!-- 이 부분을 긁어다가 index.html에 넣어주면 된다. -->
  ...
</head>
```
이전에 npm run build를 통해 index.html에 기본적인 설정이 들어가 있기때문에 추가로 안해도 되지만, Vue 프로젝트 설치 시 일부 IDE에 따라 설정이 없는 경우도 있다.

Favicon은 [여기](https://www.favicon-generator.org/)에 들어가 favicon 이미지로 변환하여 사용하면 된다.

## Vue 공부

지금까지는 HTML, Script, CSS를 별도의 페이지에서 작성하여 include하여 적용하였었다. 하지만 Vue는 **S**ingle **F**ile **C**omponent이다. 단일 파일에 HTML, Script, CSS를 정의한다. 유지보수 하기에는 개인적으로 되게 편하고 직관적이라고 생각이 되었다.

### 컴포넌트 만들어보기

신규 vue file을 만들면 3개의 작성공간이 생긴다. 
1. template
2. script
3. css

### const & let

블록 단위 {}로 변수의 범위가 제한되었음  
cont : 한번 선언한 값에 대해서 변경할 수 없음 (상수개념)  
let : 한번 선언한 값에 대해서 다시 선언할 수 없음  
위 특징들에 대해서 자세히 알아보기 전에 ES5특징 2가지를 리뷰  

### router 활용하여 component 갈아 끼우기

