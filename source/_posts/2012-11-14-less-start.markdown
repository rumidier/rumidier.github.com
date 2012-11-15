---
layout: post
title: "Less-Start"
date: 2012-11-14 17:37
comments: true
categories: Less CSS
---

## LESS - The Dynamic Stylesheet language

## 사용 환경

- 모델명    :     MacBook Pro
- 모델 식별자:	  MacBookPro8,1
- 프로세서 이름:   Intel Core i5
- 프로세서 속도:	2.3 GHz
- 메모리:	       4 GB
- 기타: homebrew, iTerm

## LESS 설치

### LESS 공식 사이트

[Less - Site](http://lesscss.org/#usage)

### npm - LESS 설치를 위한 패키지 매니저

LESS를 다운 받기 위해서는 npm 이 필요하다.

[npm 다운로드](http://nodejs.org/download/)

### LESS 설치

    $ npm install -g less
    
## LESS 사용방법

- Less 시작하기

    폴더를 생성하고 style.less 파일을 만들어 본다.

       $ mkdir Less-Start
       $ cd Less-Start
       $ touch style.less
       
- style.less 작성

{% codeblock style.less lang:css %}
  @color: #4D926F;

  #header {
    color: @color;
  }
  h2 {
    color: @color;
  }
{% endcodeblock %}

- .less -> .css 미리보기

    .less 작성후 변환하기전 올바르게 나오는지 미리 보기를 할수 있다.

       $ lessc styles.less
       
       #header {
         color: #6cc4be;
       }

- .less -> .css 변환하기

    올바르게 작성 되었다면 .less 파일을 .css 파일로 변환한다.

	   $ lessc styles.less > styles.css
	   $ ls
	   
	   styles.less styles css
