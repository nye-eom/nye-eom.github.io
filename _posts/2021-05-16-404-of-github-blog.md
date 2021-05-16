---
layout: post
title: "GitHub 404 해결방법"
author: nyeom
tags: [Git,GitHub]
---

GitHub 블로그를 업로드하는 과정에서 HTTP 404오류와 Content Security Policy:페이지 설정에 의해 리소스 로드가 차단됨:https://nye-eom.github.io/favicon.co ("img-src") 오류가 console 창에 발생했다. 이에 대한 대처 방법은 아래와 같다.

### GitHub Error Log
{% include aligner.html images="blog-img/404-of-github-blog-img.png" column=1 %}

--allow-empty instructs git commit to create a commit object that reuses the tree object of its parent. If the new commit is a root commit that does not have any parent, the tree object is a special one, the empty tree, whose SHA-1 is 4b825dc642cb6eb9a060e54bf8d69288fbee4904. The empty tree maps to an empty directory, without any sub-directories or files in it. The empty in --allow-empty means no changes have been made since the last commit or the initial state.

When an empty commit has a parent, its tree is the same with the parent's. The tree could be the empty tree or a non-empty tree, depending on the tree referenced to by the parent. When the empty commit does not have a parent, its tree is always the empty tree.

[https://stackoverflow.com/questions/62906821/does-an-empty-commit-have-an-empty-tree-in-git](https://stackoverflow.com/questions/62906821/does-an-empty-commit-have-an-empty-tree-in-git)

```yml
#git comment
git commit --allow-empty -m "rebuild"
git push origin master
```