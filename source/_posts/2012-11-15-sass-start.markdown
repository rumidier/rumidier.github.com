---
layout: post
title: "Sass 시작하기"
date: 2012-11-15 16:40
comments: true
categories:  Sass CSS
---

Sass - Syntactically Awesome Stylesheets

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

Sass의 공식 사이트 주소는 [Sass 사이트](http://sass-lang.com/docs.html) 입니다.

### gem - Sass 설치를 위한 패키지 매니저

gem을 사용하기 위해서는 Ruby가 설치되어 있어야 합니다.
[gem 설치가이드](http://octopress.org/docs/setup/rvm/)

### RVM 패키지 설치

ruby를 설치 하기전 ruby를 관리해주는 RVM 을 설치 합니다.
처음 실행 시키면 'q'를 누르라고 나옵니다. 'q' 입력후 설치 시간이 좀 걸리게 됩니다. 


    $ curl -L https://get.rvm.io | bash -s stable --ruby

    ruby-1.9.3-p327 - #extracting ruby-1.9.3-p327 to /Users/hancho/.rvm/src/ruby-1.9.3-p327
    ruby-1.9.3-p327 - #extracted to /Users/hancho/.rvm/src/ruby-1.9.3-p327
    ruby-1.9.3-p327 - #configuring
    ruby-1.9.3-p327 - #compiling
    ruby-1.9.3-p327 - #installing 
    Removing old Rubygems files...
    Installing rubygems-1.8.24 for ruby-1.9.3-p327 ...
    Installation of rubygems completed successfully.
    Saving wrappers to '/Users/hancho/.rvm/bin'.
    ruby-1.9.3-p327 - #adjusting #shebangs for (gem irb erb ri rdoc testrb rake).
    ruby-1.9.3-p327 - #importing default gemsets (/Users/hancho/.rvm/gemsets/)
    Install of ruby-1.9.3-p327 - #complete 
    Creating alias default for ruby-1.9.3-p327.
    Recording alias default for ruby-1.9.3-p327.
    Creating default links/files
    Saving wrappers to '/Users/hancho/.rvm/bin'.

    * To start using RVM you need to run `source /Users/hancho/.rvm/scripts/rvm`
    in all your open shell windows, in rare cases you need to reopen all shell windows.
    
### Ruby 설치

RVM을 정상적으로 설치가 되면 rvm 을 사용하여 루비 를 설치하여 줍니다.

    $ rvm install 1.9.3

    A RVM version 1.16.20 (stable) is installed yet 1.14.5 (stable) is loaded.
    Please do one of the following:
    * 'rvm reload'
    * open a new shell
    * 'echo rvm_auto_reload_flag=1 >> ~/.rvmrc' # for auto reload with msg.
    * 'echo rvm_auto_reload_flag=2 >> ~/.rvmrc' # for silent auto reload.

ruby 버전별 사용

ruby 버전을 최신으로 설정하여 줄수 있습니다.

    $ rvm use 1.9.3

    Using /Users/hancho/.rvm/gems/ruby-1.9.3-p327


ruby 최신 버전 적용

현재 보다 최신 버전이 있으면 최신 버전으로 적용 시켜 주게 됩니다. 일회성
현재 사용하고 있는 버전이 최신이 아니었다면 위의 $ rvm use 1.x.x 사용하여
주는게 좋습니다.

    $ rvm rubygems latest

    Removing old Rubygems files...
    Installing rubygems-1.8.24 for ruby-1.9.3-p327 ...
    Installation of rubygems completed successfully.
    
### Sass 설치

RVM과 Ruby가 정상적으로 설치되면 sass를 설치 할수 있습니다.

    $ gem install sass
    
## Sass 사용방법

- Sass 따라 해보기

    폴더를 생성하여 style.scss 파일을 만들어 봅니다.

       $ mkdir Sass-Start
       $ cd Sass-Start
       $ touch style.scss

- style.scss 파일 작성

sass가 동작 하는지 확인 하기 위하여 테스트 데이터를 작성 합니다.

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

작성된 .scss 파일을 .css 파일로 변환하여야 합니다. 다음은 .scss 파일이 변경
되었을시 재입력 없이 변경 되는 명령어 입니다.

    $ sass --watch style.scss:style.css
