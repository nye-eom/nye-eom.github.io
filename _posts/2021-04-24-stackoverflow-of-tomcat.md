---
layout: post
title: "Tomcat StackOverflowError 조치방법"
author: nyeom
tags: [Server]
---

로컬 환경에서 Tomcat 8 버전 을 다운로드 후 서버 재기동시 간헐적으로 stackOverflowError 가 발생했다. tomcat의 core component인 catalina 가 실직적인 톰캣 서버를 구동시킨다. catalina 클래스를 위한 표준 자바 프로퍼티를 정의하는 파일 내 jar 파일 스캔 제외 항목에 bcporv*.jar 파일을 추가하여 톰캣 시작 시간을 단축시킬 수 있다.

### catalina.properties 수정
```yml
---
# jar 파일 스캔 제외
tomcat.util.scan.StandardJarScanFilter.jarsToSkip=\
annotations-api.jar,\
ant-junit*.jar,\
ant-launcher.jar,\
ant.jar,\
asm-*.jar,\
aspectj*.jar,\
bootstrap.jar,\
...
bcprov*.jar
---
```