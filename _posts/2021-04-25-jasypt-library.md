---
layout: post
title: "jasypt를 이용한 properties 암복호화"
feature-img: "assets/img/blog-img/encryption-img.jpg"
thumbnail: "assets/img/blog-img/encryption-img.jpg"
tags: [Java,Spring Framework]
---

[jasypt](http://www.jasypt.org/)는 개발자가 최소한의 노력으로 암호화 작업에 대한 깊은 지식없이 애플리케이션 기본 정보를 암호화할 수 있도록 지원하는 자바 기반 라이브러리이다. 보안 취약점 정의에 부합하여 해당 라이브러리를 도입하게 되었다.

### dependencies-app.gradle 
```yml
compile rootProject.ext.dependencies.jasypt
compile rootProject.ext.dependencies.bcprov
```

### dependencies-variable.gradle 
```yml
jasypt                  : "org.jasypt:jasypt-spring31:1.9.3" ,
bcprov                  : "org.bouncycastle:bcprov-jdk16:1.45"
```

### app-datasource.xml 
```xml

<bean id="bouncyCastleProvider" class="org.bouncycastle.jce.provider.BouncyCastleProvider"/>
 
<bean id="environmentVariablesConfiguration" class="org.jasypt.encryption.pbe.config.EnvironmentStringPBEConfig">
    <property name="provider"          ref="bouncyCastleProvider" />
    <!--암호화에 사용하는 알고리즘방식 algorithm : PBEWITHSHA256AND128BITAES-CBC-BC-->
    <property name="algorithm"          value="PBEWITHSHA256AND128BITAES-CBC-BC" />
    <property name="passwordEnvName" value="APP_ENCRYPTION_PASSWORD" />
</bean>
 
 <bean id="configurationEncryptor" class="org.jasypt.encryption.pbe.StandardPBEStringEncryptor">
    <property name="config" ref="environmentVariablesConfiguration" />
    <property name="password" value="testpassword" />
</bean>
 
<bean id="propertyConfigurer" class="org.jasypt.spring31.properties.EncryptablePropertyPlaceholderConfigurer">
    <constructor-arg ref="configurationEncryptor" />
    <property name="locations">
        <list>
            <value>classpath:config/properties/config.xml</value>
        </list>
    </property>
</bean>
```


### EncryptionTest.java
```java
Security.addProvider(new BouncyCastleProvider());
 
StandardPBEStringEncryptor pbeEnc = new StandardPBEStringEncryptor();
 
pbeEnc.setProviderName("BC");
pbeEnc.setAlgorithm("PBEWITHSHA256AND128BITAES-CBC-BC"); 
pbeEnc.setPassword("testpassword");
  
String encode = pbeEnc.encrypt("password");
         
System.out.println("암호화 : "+encode);
         
String decode = pbeEnc.decrypt(encode);
         
System.out.println("복호화 : "+decode);
```


### config.xml
```xml
<!--entry key값으로 정의된 값은 ${testproject.password}형식으로 불러와 사용가능-->
<entry key="testproject.username">nyeom</entry>
<entry key="testproject.password">ENC(qyAGYmLaO5SnCnm5Dd1muZyyXodwu0uE)</entry>
```
