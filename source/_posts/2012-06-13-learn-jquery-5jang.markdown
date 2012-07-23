---
layout: post
title: "Learn jQuery 5장"
date: 2012-06-13 17:29
comments: true
categories: jQuery
---

Source
------

[예제.html](https://gist.github.com/2922803)

[예제 css ]( https://gist.github.com/2922807)

[예제 js  ](https://gist.github.com/2922804)


본문
----

## 속성 추가하기

id속성값을 개별적으로 attr()으로 적용 해주기 위해 each()를 사용하여 적용하여 주고 있다.
index는 0부터 시작하여 증가한다.

    $(document).ready(function() {
      $('div.chapter a[href*=wikipedia]').each(function(index) {
	var $thisLink = $(this);
	$(this).attr({
	  'rel': 'external',
	  'id': 'wikilink-' + index,
	  'title': $thisLink.text() + '에 대한 자세한 정보는 위키 피디아에 있습니다.'
	});
      });
    });

## 앵커 삽입

앵커 위치를 정하기 위해 body에 prependTo()로 삽입한다.
앵커 버튼이 굳이 다 있을 필요는 없고 화면 밖에 존재 부터 하기 위해
p:gt(4) 5번째(0부터 시작) 문단 부터 적용 시킨다

    $('<a href="#top">맨 앞으로 돌아가기</a>').insertAfter('div.chapter p:gt(4)');
    $('<a id="top" name="top"></a>').prependTo('body');

## 주석 표시, 숫자 부여, 컨텍스트 연결

챕터가 끝난지점 후에 리스트 목록인 &gt;ol&lt;만들어준다.
클래스가 footnote

    $('<ol id="notes"></ol>').insertAfter('div.chapter');
    $('span.footnote').each(function(index) {
      $(this).before('<a href="#foot-note-' + (index+1) +
	'" id="context-' + (index+1) + '" class="context"><sup>'
	+ (index+1) + '</sup></a>')
      .appendTo('#notes')
      .append( '&nbsp;(<a href="#context-' + (index+1) + '">context </a>)' )
      .wrap('<li id="foot-note-' + (index+1) + '"></li>');
    });

Command Action
-------------
