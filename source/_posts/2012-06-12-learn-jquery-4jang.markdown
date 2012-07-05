---
layout: post
title: "Learn jQuery 4장"
date: 2012-06-12 16:49
comments: true
categories: jQuery
---

Source
------

[예제.html](https://gist.github.com/2915965)

[예제 css ]( https://gist.github.com/2915963)

[예제 js  ](https://gist.github.com/2915969)

본문
----

## 인라인 CSS 변경

폰트 크기 구하기

    $('div.speech').css('fontSize')

반환된 값이 숫자와 단위 문자열이 합쳐져 있으므로 각각 나누기 위해 변수를 따로 저장
변수 이름에 $는 변수명에 쓰이며 jQuery객체를 저장하고 있다는 의미로 사용된다.

    var $speech     = $('div.speech');
    var currentSize = $speech.css('fontSize');

문자열에서 숫자까지만 변환하여 추출(10진수 옵션 설정)
숫자가 아니면 NaN(Not a Number)반환

    var num         = parseFloat(currentSize, 10);

fontSize의 유닛을 구함(px, em)

    var unit        = currentSize.slice(-2);

현재 클릭된 버튼의 아이디를 확인하여 숫자연산 후
css에 fontSize 적용

    if (this.id == 'switcher-large') {
      num *= 1.4;
    } else if (this.id == 'switcher-small') {
      num /= 1.4;
    }
    $speech.css('fontSize', num + unit);

{% codeblock css-part %}
$('div.button').click(function() {
  var $speech     = $('div.speech');
  var currentSize = $speech.css('fontSize');
  var num         = parseFloat(currentSize, 10);
  var unit        = currentSize.slice(-2);

  if (this.id == 'switcher-large') {
    num *= 1.4;
  } else if (this.id == 'switcher-small') {
    num /= 1.4;
  }
  $speech.css('fontSize', num + unit);
});
{% endcodeblock %}

## hide와 show

jQuery 효과에 속도를 지정할때는 'slow', 'normal', 'fast'(각각 0.6, 0.4 0.2초)를 지정할수 있으며
밀리초 단위의 시간을 조정할수 있다(근데 난 차이를 모르겠다..)

    $('document).ready(function() {
      $('div.speech p:eq(1)').hide();
      $('span.more').click(function() {
	$('div.sppech p:eq(1)').show();
	$(this).hide();
      });
    });

show는 .animate()메서드의 약식 메서드이다.

    $(document).ready(function() {
      $('p:eq(1)').hide();
      $('span.more').click(function() {
	$('p:eq(1)').animate({height: 'show', width: 'show', opactity: 'show'}, 'slow');
	$(this).hide();
      });
    });

## 사용자형 애니메이션 생성하기

버튼의 높이를 키우면서 이동, 이동이 멈추면 크기 고정

    $(document).ready(function() {
      $('div.label').click(function() {
	$('div.butoon').animate({left: 650, height: 38}, 'slow');
      });
    });

## 숫자 이해하기

height의 38값인 이유는 우리가 버튼을 50으로 만들기 위해서 이다.
css에 padding은 5px, border는 1px 로 정의 하였으므로 top + bottom값을
더한후(12) 50 - 12 = 38값이 나오게 되었다.

## CSS로 위치 변경

.animate()를 사용하여 작업할때 CSS속성이 relative 또는 absolute로 설정 되어있어야 한다
모든 블록 요소가 가지는 CSS position 속성은 static이다.

## 버튼의 너비 계산

버튼의 넓이와 패딩 보더 넓이를 모두 구하여 더해준후 div.speech p의 넓이에 맞추어서
값을 구하였다. 그렇게 함으로써 글자 오른쪽 모서리에 맞춤이 이루어 진다.

    $(document).ready(function() {
      $('div.label').click(function() {
      var paraWidth        = $('div.speech p').width();
      var $button          = $('div.button');
      var buttonWidth      = $button.width();
      var paddingRight     = $button.css('paddingRight');
      var paddingLeft      = $button.css('paddingLeft');
      var borderRightWidth = $button.css('borderRightWidth');
      var borderLeftWidth  = $button.css('borderLeftWidth');

      //총너비 연산
      var totalButtonWidth =
      parseInt(buttonWidth, 10) +
      parseInt(paddingRight, 10) +
      parseInt(paddingLeft, 10) +
      parseInt(borderRightWidth, 10) +
      parseInt(borderLeftWidth, 10);
      var rightSide = paraWidth - totalButtonWiidth;
      $button.animate({left: rightSide, height: 38}, 'slow');
      });
    });

## 동시효과

불투명해짐과 배경색이 동시에 변경되며 이동을 한후 불투명도가 들어오고 사라지게 된다

    $('div.label').click(function() {
      $('div.button')
      .fadeTo('slow', 0.5)
      .animate({left: 650}, 'slow')
      .fadeTo('slow', 1.0)
      .css('backgroundColor', '#f00')
      .slideUP('slow');
    });

## 연속효과

버튼을 클릭 하게 되면 투명해지고 이동한다. 그리고 투명도를 다시 돌리고나서
배경색을 변경한다. 그리고 사라진다 이게 연속적으로 이루어 지게 되어있다.
콜백을 이용하여 효과들이 모두 진행된 후에 그 다음 순서로 배경색을 바꾸는
비효과 메서드를 적용 하였다.

    $('div.label').click(function() {
      $('div.button')
      .fadeTo('slow', 0.5)
      .animate({left: 650}, 'slow')
      .fadeTo('slow', 1.0, function() {
	$(this).css('backgroundColor', '#f00')
      }).slideUP('slow');
    });

## 다중 효과

    $('div.speech p:eq(3)').css('backgroundColor', '#fcf').hide();
    $('div.speech p:eq(2)').css('backgroundColor', '#cff').click(function() {
      var $thisPar = $(this)
      $(this).next().slideDown('slow', function() {
	$thisPar.slideUp('slow');
      });
    });


Command action
-----------

- fadeIn()과 fadeOut(): 불투명도(opacity)

  **fadeOut(speed, callback)**

  일치하는 엘리먼트 중 드러난 엘리먼트의 불투명도 0%로 줄여가면서 화면에서 제거한다. 불투명
  도가 변경되는 지속시간은 speed 매개변수에 따라 변한다. 이미 감춰진 엘리먼트는 영향을 받지 않
  는다.

  **매개변수**

  speed

  (Numbe|String)효과의 지속 시간을 1/1000초 단위의 숫자 또는 미리 정의된 문자열 slow, normal, fast

  가운데 하나로 명시한다. 생략되면 기본값인 normal을 이용한다.

  callback

  (Function) 선택사항으로 애니메이션이 완료된 뒤 호출되는 함수다. 이 함수는 어떤 매개변수도
  받지 않는다. 하지만 애니메이션이 수행되는 엘리먼트가 함수 콘텍스트인 this로 설정된다.

  **반환값**

  확장집합

- fadeTo: 불투명도(opacity)

  **fadeOut(speed, opacity, callback)**

  확장 엘리먼트의 불투명도를 현재의 러정 값에서 opacity 매개변수 값으로 설정한다.

  **매개변수**

  speed

  (Numbe|String)효과의 지속 시간을 1/1000초 단위의 숫자 또는 미리 정의된 문자열 slow, normal, fast

  가운데 하나로 명시한다. 생략되면 기본값인 normal을 이용한다.

  opacity (Number)

  (Number) 0.0에서 1.0 사이의 값으로 엘리먼트에 적용될 불투명도 값

  callback

  (Function) 선택사항으로 애니메이션이 완료된 뒤 호출되는 함수다. 이 함수는 어떤 매개변수도
  받지 않는다. 하지만 애니메이션이 수행되는 엘리먼트가 함수 콘텍스트인 this로 설정된다.

  **반환값**

  확장집합

- slideDown()과 slideUp(): 높이(height)

  **slideDown(speed, callback)**

  감춰진 모든 일치하는 엘리먼트가 높이 값이 증가하면서 나타난다. 드러나 잇는 엘리먼트는
  영향을 받지 않는다

  **매개변수**

  speed

  (Numbe|String)효과의 지속 시간을 1/1000초 단위의 숫자 또는 미리 정의된 문자열 slow, normal, fast

    가운데 하나로 명시한다. 생략되면 기본값인 normal을 이용한다.

  callback

    (Function) 선택사항으로 애니메이션이 완료된 뒤 호출되는 함수다. 이 함수는 어떤 매개변수도
    받지 않는다. 하지만 애니메이션이 수행되는 엘리먼트가 함수 콘텍스트인 this로 설정된다.

  **반환값**

  확장집합

  **slideDown(speed, callback)**

  감춰진 모든 일치하는 엘리먼트가 점차적으로 높이 값이 감소하면서 화면에서 제거된다.

  **매개변수**

  speed

    (Numbe|String)효과의 지속 시간을 1/1000초 단위의 숫자 또는 미리 정의된 문자열 slow, normal, fast

    가운데 하나로 명시한다. 생략되면 기본값인 normal을 이용한다.

  callback

    (Function) 선택사항으로 애니메이션이 완료된 뒤 호출되는 함수다. 이 함수는 어떤 매개변수도
    받지 않는다. 하지만 애니메이션이 수행되는 엘리먼트가 함수 콘텍스트인 this로 설정된다.

  **반환값**

  확장집합
