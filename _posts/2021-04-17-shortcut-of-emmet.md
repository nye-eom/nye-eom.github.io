---
layout: post
title: "Emmet 단축키"
author: nyeom
tags: [IDE]
---


[Emmet](https://emmet.io/)은 Text Editor에 기본적으로 설치되어 있는 플러그인으로 HTML 작성속도를 크게 향상 시켜주는 자동완성 기능을 제공한다.

```html
<!--명령어 : !+Tab -->
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
		<!--명령어 : div.userClass+Tab -->
    <div class="userClass"></div>
		<!--명령어 : div#userId+Tab -->
		<div id="userId"></div>
		<!--명령어 : div>ul>li+Tab -->
		<div>
			<ul>
				<li></li>
			</ul>
		</div>
		<!--명령어 : div>ul+ol+Tab -->
		<div>
			<ul></ul>
			<ol></ol>
		</div>		
		<!--명령어 : ul>li*5+Tab -->
		<ul>
			<li></li>
			<li></li>
			<li></li>
			<li></li>
			<li></li>
		</ul>
		<!--명령어 : div>ul>li^ol+Tab -->
		<div>
			<ul>
				<li></li>
			</ul>
			<ol></ol>
		</div>	

		<!--명령어 : div>(header>ul>li*2>a)+footer>p + Tab -->
		<div>
        <header>
            <ul>
                <li><a href=""></a></li>
                <li><a href=""></a></li>
            </ul>
        </header>
        <footer>
            <p></p>
        </footer>
    </div>

		<!--명령어 : p{hello} + Tab -->
		<p>hello</p>

		<!--명령어 : p.class${item $}*5 + Tab -->
		<p class="class1">item 1</p>
    <p class="class2">item 2</p>
    <p class="class3">item 3</p>
    <p class="class4">item 4</p>
    <p class="class5">item 5</p>

		<!--명령어 : p>lorem + Tab -->
		<!--dummy text -->
		<p>Lorem, ipsum dolor sit amet consectetur adipisicing elit. Ab accusantium similique minus sunt reiciendis ut nobis repellat facere porro et at, expedita totam ad, beatae aliquid. Quisquam nulla voluptatum exercitationem.</p>

		<!--명령어 : p>lorem4 + Tab -->
		<p>Lorem, ipsum dolor sit.</p>
</body>
</html>
```
