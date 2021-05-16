---
layout: post
title: "CI/CD의 정의"
author: nyeom
tags: [CI/CD]
---

애플리케이션 개발단계를 자동화하여 애플리케이션을 보다 짧은 주기로 고객에게 제공하는 방법으로 애플리케이션의 통합 및 테스트 단계에서부터 제공 및 배포에 이르는 애플리케이션의 라이프사이클 전체에 걸쳐 지속적인 automation와 지속적인 monitoring을 제공한다.

### CI(Continuous Integration)
개발자를 위한 자동화 프로세스인 지속적인 통합을 의미하며 애플리케이션에 대한 새로운 코드 변경 사항이 정기적으로 build 및 test되어 공유 repository에 통합되므로 여러명의 개발자가 동시에 애플리케이션 개발과 관련된 코드작업을 할 경우 서로 conflict 할 수 있는 문제를 해결할 수 있다.


### CD(Continuous Delivery/Deployment)
지속적인 서비스 제공 및 지속적인 배포를 의미하며 애플리케이션에 적용된 변경사항이 버그 테스트를 거쳐 repository(ex. gitHub, gitLab etc) 에 자동으로 업로드되는 것을 뜻하며 운영팀은 해당 repository에서 애플리케이션을 실시간 product 환경까지 자동 배포할 수 있다. 또한 실제 배포해야할 애플리케이션 서버가 여러대일 경우, 원클릭으로 빌드, 테스트, 배포 자동화를 진행할 수 있다.

### CI/CD Pipeline
![image](https://www.redhat.com/cms/managed-files/styles/wysiwyg_full_width/s3/ci-cd-flow-desktop_edited_0.png?itok=TzgJwj6p)

DevOps 또는 SRE(Site Reliability Engineer) 방식을 통해 더 효과적으로 소프트웨어를 제공하는데 초점을 맞춘 방법으로 개발 머신에서 테스트와 스테이징을 거쳐 최종적으로 출시하여 사용자에게 전달하기 위해 코드가 거치는 일련의 단계이다.