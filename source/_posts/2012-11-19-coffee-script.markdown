---
layout: post
title: "Coffee Script 시작하기"
date: 2012-11-19 12:23
comments: true
categories: CoffeeScript JS
---

### 사용 환경

  - 모델명    :     MacBook Pro
  - 모델 식별자:	  MacBookPro8,1
  - 프로세서 이름:   Intel Core i5
  - 프로세서 속도:	2.3 GHz
  - 메모리:	       4 GB
  - 기타: homebrew, iTerm

### CoffeeScript 설치

CoffeeScript - CoffeeScript is a little language that compiles into JavaScript

### CoffeeScript 공식 사이트

CoffeeScript 공식 사이트 주소는 [CoffeeScript 사이트](http://coffeescript.org/)
입니다.

### npm - coffee-script 설치를 위한 패키지 매니저

coffee-script를 다운 받기 위해서는 npm이 필요 하고 별도로 설치 해야 하며
`npm` 설치를 위한 파일은 아래의 링크에서 다운로드 받습니다.

[npm 다운로드](http://nodejs.org/download/)

### node-v.8.x.x.pkg 설치

개인 OS에 맞는 파일을 선택해 다운 받고 설치 합니다. 다음은 Mac 에서의
`.pkg` 실행시 첫화면과 마지막 화면 입니다.

{% img https://lh5.googleusercontent.com/-eUicOa-fhtQ/UKXCFOGz27I/AAAAAAAAACE/9LBj6Kzdn-8/%25252FUsers%25252Fhancho%25252FPictures%25252Fnode-01.jpg 500 500 "node.pkg 설치 시작" %}
{% img https://lh5.googleusercontent.com/-Smr4TJfxMgI/UKXEkWDOYWI/AAAAAAAAACM/soEN5qpthGg/%25252FUsers%25252Fhancho%25252FPictures%25252Fnode-02.jpg 500 500 "node.pkg 설치 끝" %}

### coffee-script 설치

`npm`을 사용해 `coffee-script`를 설치해 줍니다.

	hancho@hanjoui-MacBook-Pro:~$ sudo npm install -g coffee-script
	Password:
	npm http GET https://registry.npmjs.org/coffee-script
	npm http 304 https://registry.npmjs.org/coffee-script
	/usr/local/bin/coffee -> /usr/local/lib/node_modules/coffee-script/bin/	coffee
	/usr/local/bin/cake -> /usr/local/lib/node_modules/coffee-script/bin/cake
	coffee-script@1.4.0 /usr/local/lib/node_modules/coffee-script

### CoffeeScript 사용방법

#### CoffeeScript 시작하기

    테스트를 위한 폴더를 생성후 `style.less` 파일을 만듭니다.

       $ mkdir Coffee-Start
       $ cd Coffee-Start
       $ touch style.coffee

#### style.coffee 작성

`coffee`가 동작 확인을 위해 테스트 파일를 작성합니다.

{% codeblock style.coffee lang:js %}
fill = (container, liquid = "coffee") ->
  "Filling the #{container} with #{liquid}..."

alert fill("cup")
{% endcodeblock %}

#### .coffee -> .js 변환하기

  .coffee 파일 작성후 .js 파일로 변환합니다. 파일명은 style.coffee의 style.js로 변환됩니다.

        $ coffee --compile style.coffee
        $ ls
        style.coffee style.js

#### .coffee -> .js 지켜보기

  `--watch` 옵션으로 style.coffee 파일 내용이 갱신(저장)시 
  `.js`파일로 변환 됩니다. 종료는 Ctrl + C 키로 할수있습니다.

        $ coffee --watch --compile style.coffee
        11:55:26 - compiled style.coffee

#### coffeescript - .coffee 확인 하기

`.html` 파일 내에서 `.js` 파일로 변환 없이 .coffee를 검사 할수있습니다.

{% codeblock coffee.html %}
<html>
  <head>
  <script src="http://jashkenas.github.com/coffee-script/extras/coffee-script.js" type="text/javascript" charset="utf-8"></script>
  <script type="text/coffeescript">
    fill = (container, liquid = "coffee") ->
      "Filling the #{container} with #{liquid}..."

    alert fill("cup")
  </script>
  </head>

  <body>
  </body>
</html>
{% endcodeblock %}

#### coffeescript - .js 확인하기

`.html` 파일 내에서 변환된 `.js` 내용을 검사 할수있습니다.

{% codeblock coffee.html %}
<html>
  <head>
  <script src="http://jashkenas.github.com/coffee-script/extras/coffee-script.js" type="text/javascript" charset="utf-8"></script>
  <script>
    var fill;

    fill = function(container, liquid) {
      if (liquid == null) {
        liquid = "coffee";
      }

      return "Filling the " + container + " with " + liquid + "...";
    };

    alert(fill("cup"));
  </script>
  </head>

  <body>
  </body>
</html>
{% endcodeblock %}
