---
layout: post
title: "LESS 시작하기"
date: 2012-11-14 17:37
comments: true
categories: LESS CSS
---

## LESS - The Dynamic Stylesheet Language

## 사용 환경

- 모델명    :     MacBook Pro
- 모델 식별자:	  MacBookPro8,1
- 프로세서 이름:   Intel Core i5
- 프로세서 속도:	2.3 GHz
- 메모리:	       4 GB
- 기타: homebrew, iTerm

## LESS 설치

### LESS 공식 사이트

LESS의 공식 사이트 주소는 [LESS 사이트](http://lesscss.org/#usage) 입니다.

### npm - LESS 설치를 위한 패키지 매니저

LESS를 다운 받기 위해서는 npm이 필요 하고 별로도 설치를 해주어야 합니다.
npm 설치를 위해 필요한 파일은 아래의 링크에서 다운로드 받을수 있습니다.

[npm 다운로드](http://nodejs.org/download/)

### node-v.8.x.x.pkg 설치

개인의 OS에 맞는 파일을 선택하여 다운 받았다면 이를 설치 하여 줍니다. 다음은 Mac 에서의
.패키지 실행시 첫화면과 마지막 화면 입니다.

{% img https://lh5.googleusercontent.com/-eUicOa-fhtQ/UKXCFOGz27I/AAAAAAAAACE/9LBj6Kzdn-8/%25252FUsers%25252Fhancho%25252FPictures%25252Fnode-01.jpg 500 500 "node.pkg 설치 시작" %}
{% img https://lh5.googleusercontent.com/-Smr4TJfxMgI/UKXEkWDOYWI/AAAAAAAAACM/soEN5qpthGg/%25252FUsers%25252Fhancho%25252FPictures%25252Fnode-02.jpg 500 500 "node.pkg 설치 끝" %}

### LESS 설치

패키지 설치가 정상적으로 이루어 지면 npm을 사용LESS를 설치 할수 있습니다.

    $ npm install -g less
    
## LESS 사용방법

- LESS 시작하기

    폴더를 생성하고 style.less 파일을 만들어 봅니다.

       $ mkdir Less-Start
       $ cd Less-Start
       $ touch style.less
       
- style.less 작성

less가 제대로 동작하는지 확인 하기 위하여 테스트 데이터를 작성 합니다.

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

    .less 작성후 변환하기전 올바르게 나오는지 미리 보기를 할수 있습니다.

       $ lessc styles.less
       
       #header {
         color: #6cc4be;
       }

- .less -> .css 변환하기

    올바르게 작성 되었다면 .less 파일을 .css 파일로 변환하여 줍니다.

	   $ lessc styles.less > styles.css
	   $ ls
	   
	   styles.less styles css
