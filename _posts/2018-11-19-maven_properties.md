---
layout: customize-posts
title: "Maven DB(Mysql) 연동하기 "
category:
    - Java
tags:
    - Java
    - Maven
    - Properties
    - Mysql
published: false
---

># Maven Properties 설정
*   기본적으로 properties 파일을 관리하는 가장 큰 이유는 내가 생각하기에 개발환경 별 코드수정을 최소화 하기에 필요한 부분 이다. 예를 들어 실제 운영되는 서비스의 경우 Test, Dev, Real 최소 3단계로 이루어 진다.
    1.   Test는 말 그대로 로컬에서 개발을 통하여 테스트를 하는 곳.
    2.   Dev는 개발 완료 후 Real로 적용 전 단위테스트, E2E(End to End) 테스트 등... 전반적으로 운영서비스에 반영 전 부분적 or 전체적으로 테스트 하는 곳.
    3.   Real은 실제 운영서비스에 반영 되는 곳.
* 각 서비스 환경 별 테스트 환경도 각기 다를 뿐 아니라 접속정보도 상이하다. 그러 한 정보를 소스에 하드코딩이 되 있을 경우 매번 소스를 찾아 수정하기가 사실상 어려운 부분이다. 이럴 때 properties를 별도로 설정 및 구성하여 소스 수정없이 각 단계 및 환경 별 적용을 위함이 가장 큰 이유로 생각 된다.

>## properties 설정
*   1. 기본적으로 pom.xml에 최초 설정을 한다.
    ```xml
        <!-- build 안에 아래와 같이 설정 -->
        <!-- ~/resources* properties files setting -->
        <resources>
            <resource>
                <directory>src/main/resources/</directory>
                <filtering>true</filtering>
            </resource>
            <resource>
                <directory>src/main/resources/${env}</directory>
            </resource>
        </resources>
    ```
*   2. pom.xml profile 추가
    ```xml
        <!-- <activeByDefault>은 패키지시에 특별한 명령어가 없다면 기본 프로파일이 된다. -->
        <profiles>
            <profile>
                <id>dev</id>
                <activation>
                    <activeByDefault>true</activeByDefault>
                </activation>
                <properties>
                    <env>dev</env>
                </properties>
            </profile>
            <profile>
                <id>real</id>
                <properties>
                    <env>real</env>
                </properties>
            </profile>
        </profiles>
    ```
    *   Tip) Maven에 환경변수를 지정하는 방법은 아래 2가지 방식이 있다.
    ```xml
        <!-- 첫 번째 방법 -->
        <properties>
        <!-- -P 로 명시하지 않을 경우 기본 프로파일 -->
            <env>dev</env>
        </properties>


        <!-- 두 번째 방법 -->
        <profile>
            <id>dev</id>
            <activation>
                <activeByDefault>true</activeByDefault>
            </activation>
            <properties>
                <env>dev</env>
            </properties>
        </profile>
    ```

*   1. root-context.xml 추가
    ```xml
        <bean class= "org.springframework.beans.factory.config.PropertyPlaceholderConfigurer" >
            <property name= "locations">
                <!-- 밑에 classpath 은 pom.xml에 설정하였다. -->
                <!-- <directory>src/main/resources/${env}</directory> -->
                <!-- 위의 설정으로 인해 classpath가 src/main/resources/dev/ 로 설정이 됨 -->
                <value>classpath:config.properties</value >
            </property>
        </bean>
    ```
*   2. root-context.xml에 DB연결 접속정보 셋팅
    ```xml
        <bean id="dataSource" class="org.apache.commons.dbcp2.BasicDataSource"> 
            <property name="driverClassName" value="${jdbc.driverClassName}"/> 
            <property name="url" value="${jdbc.url}"/> 
            <property name="username" value="${jdbc.username}"/> 
            <property name="password" value="${jdbc.password}"/>
        </bean>
    ```

*   1. config.properties 생성
    ```xml
        #dev properties file

        jdbc.driverClassName=com.mysql.jdbc.Driver
        jdbc.url=jdbc:mysql://127.0.0.1:3306/devweb01
        jdbc.username=ID
        jdbc.password=Password
    ```

*   위의 pom.xml, root-context.xml, config.properties file을 설정을 완료하게 되면 properties file 설정이 완료되며, 소스수정을 최소화하여 환경설정을 개발환경에 맞게 변경할 수 있다.

