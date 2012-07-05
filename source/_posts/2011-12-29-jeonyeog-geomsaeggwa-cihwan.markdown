---
layout: post
title: "전역 검색과 치환"
date: 2011-12-29 22:24
comments: true
categories: 
---

### 전역 검색과 치환

버퍼의 x행과 효애 사이에서 패턴(pattern)을 찾아 치환 문자열(replacement)로 까누다
패턴은 정규 표현식이다.

1~10번째 줄에서 weeble르 wobble로 대체한다.

    :[x,y]s/patern/replacement/flags
    :1,10s/weeble/wobble

### 마크 하기

어떤 위치에서 ma라고 입력하면 그 위치에 a 표시(mark)을 한다

a표시로 이동

    `a

a표시행의 맨앞으로 이동

    'a

마크를 이용한 줄에서의 치환
'a행에서 .현재 행을 의미

    :'a, .s/weeble/wobble/

마크를 사용한 복사와 삭제
복사를 시작할 위치에서 y를 누르고 `a를 사용하게 되면 현재 위치에서 마크위치까지를
복사하게 된다(삭제는 y대신 d사용)

     :y`a

레지스터에 저장하기
a-z, A-Z를 사용가능 하며 소문자는 한개만 대문자는 기존에 추가 된다

    "ayy : 한줄 저장
    "ay`a : 현재 행부터 마크까지 저장
