---
layout: post
title: "Spring Cloud Netflix Ribbon vs Zuul"
author: nyeom
tags: [Java,Spring Framework,Cloud]
---

클라우드 기반 개발환경에서 프로젝트를 수행하며 API Gateway를 수행할 모듈로 Spring Cloud Netflix Zuul을 사용했다. 이후 Spring Framework 버전이 지속적으로 올라가면서 Netflix Zuul 은 4버전 이후 deprecated 된 상태로 더 이상의 유지보수가 되지 않는 상태가 되면서 Spring Cloud APIGateway 가 이를 대체해서 사용하고 있다. 

### Spring Cloud Netflix Zuul - *.yaml
Spring Cloud APIGateway의 경우, 동기방식 내장서버인 Tomcat이 실행된다. Netflix Zuul의 경우, 클라이언트가 호출하는 URL 규칙은 yml 에서 정의한 방식에 준한다.
```yml
server:
  port: 8000

spring:
  application:
    name: my-zuul-service

zuul:
  routes:
		#zuul이라는 API가 8000 포트로 first-service라는 요청이 올 경우,8081 port 로 포워딩
    first-service: 
			path: /first-service/**
			url: http://localhost:8081
    second-service:
			path: /second-service/**
			url: http://localhost:8082

```

### Spring Cloud Netflix Zuul - ZuulServiceApplication.java
```java
package com.example.userservice;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.cloud.netflix.zuul.EnableZuulProxy;

@SpringBootApplication
@EnableZuulProxy
public class ZuulServiceApplication {

    public static void main(String[] args) {
        SpringApplication.run(ZuulServiceApplication .class, args);
    }

}

```

### Spring Cloud Netflix Zuul - *Filter.java
```java
package com.example.userservice;

import com.netflix.zuul.ZuulFilter;
import lombok.extern.slf4j.Slf4j
import org.springframework.stereotype.Component;
import javax.servlet.http.HttpServletRequest;

@Slf4j
@Component
public class ZuulLoggingFilter extends ZuulFilter {

		Logger logger = LoggerFactory.getLogger(ZuulLoggingFilter.class);
		
		@Override
    public String filterType() {
        return "pre";
    }

		@Override
    public int filterOrder() {
        return 1;
    }

		@Override
    public boolean shouldFilter {
        return false;
    }

		@Override
    public Object run() throws ZuulException {
        RequestContext ctx = RequestContext.getCurrentContext();
				HttpServletRequest request = ctx.getRequets()
    }

}
```

### Spring Cloud APIGateway - *.yaml
Spring Cloud APIGateway의 경우, 비동기방식 내장서버인 Netty가 실행된다. Spring Cloud APIGateway의 경우, 각 마이크로 서비스 어플리케이션에서 정의한 Controller의 RequestMapping 값을 기준으로 정의한다.
```yml
server:
  port: 8000

eureka:
  client:
    register-with-eureka: false
    fetch-registry: false
    service-url:
      defaultZone: http://localhost:8761/eureka


spring:
  application:
    name: apigateway-service
  cloud:
    gateway:
      routes:
        - id: first-service
          uri: http://localhost:8081
          #조건절
          predicates:
            - Path=/first-service/**
        - id: second-service
          uri: http://localhost:8081
          predicates:
            - Path=/second-service/**
```