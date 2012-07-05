---
layout: post
title: "Learn jQuery 3장"
date: 2012-06-11 18:17
comments: true
categories: Learn jQuery
---

Source
------

[예제.html](https://gist.github.com/2909211)

[예제 css ]( https://gist.github.com/2909213)

[예제 js  ](https://gist.github.com/2909224)

본문 - 이벤트 트리거 사용하는 방법
----

## button click event

페이지 시작시 노말페이지로 보이도록 모든 클래스를 해제한다.
removeClass()는 다른 파악되지 않은 Class까지 해제 하지만 현재 예제
코드 에서는 생각치 않도록 쓴다.

    $('body').removeClass();

현재 버튼이 클릭된 id값을 확인하여 일치 하였을경우
클래스를 추가 하도록 한다.

    if (this.id == 'switcher-narrow') {
      $('body').addClass('narrow');
    }
    else if (this.id == 'switcher-large') {
      $('body').addClass('large');
    }

강조되는 글씨를 표현하기 위해 우선 클래스를 해제하고
현재 버튼에 클래스를 추가 해준다.

    $('#switcher .button').removeClass('selected');
    $(this).addClass('selected');

이벤트 객체 사용시 버블링을 중단 하기 위해 다음과 같이 추가해 준다.
(버블링을 추가안해줄시 노말 버튼 클릭시에도 버튼칸이 사라지게 된다.)

    event.stopPropagation();

부분 코드 

{% codeblock 부분코드 - 01 %}
$('#switcher .button').click(function(event) {
  $('body').removeClass();

  if (this.id == 'switcher-narrow') {
    $('body').addClass('narrow');
  }
  else if (this.id == 'switcher-large') {
    $('body').addClass('large');
  }

  $('#switcher .button').removeClass('selected');
  $(this).addClass('selected');

  event.stopPropagation();
});
{% endcodeblock %}

## 버튼 강조하기

버튼에 hover(마우스 가져다 대면) 띠면(체인으로) hover삭제

부분 코드 

{% codeblock 부분코드 %}
  $('#switcher .button').hover(function() {
    $(this).addClass('hover');
    }, function() {
      $(this).removeClass('hover');
  });
{% endcodeblock%}

## 이벤트 핸들러

핸들러를 나중에 다시 사용할 수 있도록 핸들러 함수에 이름을 부여

    var toggleStyleSwitcher = function() {
      $('switcher .button').toggleClass('hidden');
    };

핸들러를 활성화 시켜준다.

    $('#switcher').click(toggleStyleSwitcher);

노말 상태에서만 토글 기능 활성화

    $('switcher-normal').click(function() {
      $('#switcher').click(toggleStyleSwitcher);
    });

    $('#switcher-narrow, #switcher-large').click(function() {
      $('#switcher').unbind('click', toggleStyleSwitcher);
    });

시작시 접힘 기능(인자를 지정하지 않는경우 히벤트에 해당하는 행위를 발생시킴)

    $('#switcher').click();

Command action
-----------

**unbind(event Type, listener)**

**unbind(event)**

확장 집합의 모든 엘리먼트에서 전달된 매개변수에 따라 핸들러를 선택적으로 제거한다.

매개변수를 제공하지 않으면 엘리먼트의 모든 리스터를 제거한다.

**매개변수**

  **eventType**

       (String)매개변수를 제공하면 지정된 이벤트 타입에 할당된 리스너만 제거한다.

  **listener**

      (Function)매개변수를 제공하면 지정된 리스너와 동일한 것만 제거한다.

  **eventType**

      (Event) Event 인스턴스의 정보로 알 수 있는 이벤트가 발생했을 대 호출될 리스너를
      제거한다

**반환값**

확장 집합
