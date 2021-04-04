---
layout: post
title: "Maven 이란?"
author: nyeom
tags: [형상관리]
---


Java Build Tool로써 Ant, Maven, Gradle 등이 존재한다. Maven은 Build Tool만을 제공뿐만 아니라 프로젝트 Lifecycle을 관리 또한 가능하다.
필요한 라이브러리를 [Maven Repository](https://mvnrepository.com/)에서 찾아 pom.xml에 정의해주면 필요한 라이브러리 뿐만 아니라 라이브러리 동작에 필요한 하위 라이브러리까지 네트워크를 통해 자동으로 다운받아진다. 

### 시작하기에 앞서...
![image](https://maven.apache.org/images/maven-logo-black-on-white.png)\
[Maven](https://maven.apache.org/)은 유효성검증, 코드생성, 컴파일, 테스트, 패키징, 통합테스트, 확인, 설치, 배치 및 프로젝트 사이트 작성 및 배치를 포함한 프로젝트 라이프사이클의 모든 단계를 처리한다. 프로젝트 빌드관리에 사용되는 대표적인 도구로 정해진 Lifecycle에 의해 작업을 수행한다. Lifecycle에는 clean, build, site 세가지로 구성된다. 그 중 build 과정에 속하는 대상은 compile, test, package, deploy가 있다. Maven에 대한 기본적인 개념 plugin, phase, goal, lifecycle에 대한 상세 내용은 아래와 같다.

### maven plugin

Maven에서 제공하는 모든 기능은 plugin을 기반으로 동작하며 plugin은 하나 이상의 goal의 집합체이다.

### maven phase

build 라이프 사이클에서 빌드단계와 각 단계의 순서만을 정의하고 있는 개념으로 실질적인 build 작업은 phase에 연결되어 있는 플러그인의 goal 이 한다.

ex) mvn clean comiler:compile

위 예시는 clean phase를 실행하여 complier 플러그인의 compiler goal을 실행한다고 정의할 수 있다.

### maven lifecycle

기본 default lifecycle은 아래와 같이 정의된다.

```html
<phases>
      <phase>validate</phase>
      <phase>initialize</phase>
      <phase>generate-sources</phase>
      <phase>process-sources</phase>
      <phase>generate-resources</phase>
      <phase>process-resources</phase>
      <phase>compile</phase>
      <phase>process-classes</phase>
      <phase>generate-test-sources</phase>
      <phase>process-test-sources</phase>
      <phase>generate-test-resources</phase>
      <phase>process-test-resources</phase>
      <phase>test-compile</phase>
      <phase>process-test-classes</phase>
      <phase>test</phase>
      <phase>prepare-package</phase>
      <phase>package</phase>
      <phase>pre-integration-test</phase>
      <phase>integration-test</phase>
      <phase>post-integration-test</phase>
      <phase>verify</phase>
      <phase>install</phase>
      <phase>deploy</phase>
    </phases>
```


### Maven 유용한 명령어

명령어 구성은 아래와 같다.
* mvn [-option][<goal(s)>][<phase(s)>]


```bash
#Maven 버전 확인
mvn -v

#빌드시 생성되었던 output 및 파일들을 삭제
mvn clean

#컴파일 수행 (./target/classes 디렉토리에 생성)
mvn compile

#유닛테스트 수행 (./target/test-classes 디렉토리에 생성)
mvn test

#실제 컴파일된 소스 코드와 리소스들을 jar파일 등의 배포를 위한 패키지로 생성
mvn package

#유닛테스트 코드 제외해 패키지 생성
mvn package -Dmaven.test.skip=true

#패키지를 로컬 저장소에 설치
mvn install

#dependency 플러그인에서 tree 기능을 실행시켜 프로젝트 dependency Tree 형식 조회
mvn dependency:tree

#springboot 프로젝트 서버 기동
mvn spring-boot:run

```
