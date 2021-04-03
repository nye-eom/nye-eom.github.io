---
layout: post
title: "GitHub 블로그 세팅"
feature-img: "assets/img/blog-img/github-img.jpg"
thumbnail: "assets/img/blog-img/github-img.jpg" 
tags: [Git,GitHub]
---

기술블로그를 선택하는데 티스토리, velog, WordPress 등 다양한 플랫폼 중 gitHub와 Jekyll을 활용해 개인블로그를 운영하는 것을 선택했다.


### 시작하기에 앞서...


Notion을 활용해 개인적으로 공부하던 내용이나 프로젝트를 수행하며 접한 기술에 대한 설명 및 이슈 대응에 대한 내용을 정리하는 편이었다. 
그러나 정리되지 않은 채 우후죽순으로 늘어가고만 있어 기술블로그를 별도로 운영하면서 개념들을 재정리하고 
프로젝트를 수행하면서 맞닥드렸던 어려움과 해결했던 과정들을 회상하고 싶다는 마음에 결심을 하게 되었다. 

### 필수설치 프로그램

1. [VSCode](https://code.visualstudio.com/download)
2. [Git](https://git-scm.com/downloads)
3. [Ruby+DevKit](https://rubyinstaller.org/downloads/)


### Jekyll Theme 선택

Jekyll은 HTML, Markdown 등 다양한 포맷의 텍스트들을 읽고 가공해 웹사이트에 바로 게시하게 해줄수 있는 Rubby 언어 기반의 텍스트 변환 엔진이다. Jekyll은 GitHub의 내부엔진이기에 GitHub 페이지에서 별도의 세팅없이 정상적으로 동작한다. Jekyll 테마를 선택 후 프로젝트를 로컬 디렉토리에 복사한다.

1. [http://jekyllthemes.org/](http://jekyllthemes.org/)
2. [https://jamstackthemes.dev/](https://jamstackthemes.dev/)
3. [http://themes.jekyllrc.org/](http://themes.jekyllrc.org/)


### VSCode Terminal 입력 명령어
```bash
# Jekyll 세팅
gem install jekyll bundler


# git 설치 및 origin 저장소 push
git init
git remote add origin "[GitHub 사용자명].github.com"
git add .
git commit -m "message 명"
git push -u origin master

##local 서버 (http://127.0.0.1:4000/) 구동
bundle exec jekyll serve
```

### CSS 깨질 경우, config.yml 변경
```yaml
# SITE CONFIGURATION
baseurl: ""
url: "https://[GitHub사용자명].github.io"
```