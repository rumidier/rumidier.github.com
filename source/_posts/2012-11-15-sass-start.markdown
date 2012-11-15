---
layout: post
title: "Sass-Start"
date: 2012-11-15 16:40
comments: true
categories:  Sass CSS
---

ass - Syntactically Awesome Stylesheets

## 사용 환경

---------------

- 모델명    :     MacBook Pro
- 모델 식별자:	  MacBookPro8,1
- 프로세서 이름:   Intel Core i5
- 프로세서 속도:	2.3 GHz
- 메모리:	       4 GB
- 기타: homebrew, iTerm

## Sass 설치

------------------

### Sass 공식 사이트

[Sass 사이트](http://sass-lang.com/docs.html)

### gem - Sass 설치를 위한 패키지 매니저

gem을 사용하기 위해서는 Ruby가 설치되어 있어야 합니다.
[gem 설치가이드](http://octopress.org/docs/setup/rvm/)

### gem - RVM 설치

    $ curl -L https://get.rvm.io | bash -s stable --ruby
    
### gem - Ruby 설치

    $ rvm install 1.9.3
    $ rvm use 1.9.3
    $ rvm rubygems latest
    
### Sass 설치

RVM과 Ruby가 잘 설치 되었다면 이상없이 sass가 설치 될것입니다.

    $ gem install sass
    
## Sass 사용방법

- Sass 따라 해보기

    폴더를 생성하여 style.scss 파일을 생성하여 본다.

       $ mkdir Sass-Start
       $ cd Sass-Start
       $ touch style.scss

- style.scss 파일 작성

{% codeblock style.scss lang:css %}
.fakeshadow {
  border: {
    style: solid;
    left: {
      width: 4px;
      color: #888;
    }
    right: {
      width: 2px;
      color: #ccc;
    }
  }
{% endcodeblock %}

- .scss -> .css 변환하기

작성된 .scss 파일을 .css 파일로 변환하여야 합니다.

    $ sass --watch style.scss:style.css
