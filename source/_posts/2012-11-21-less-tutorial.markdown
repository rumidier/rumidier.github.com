---
layout: post
title: "Less tutorial"
date: 2012-11-21 12:44
comments: true
categories: LESS CSS
---
## Tutorial

### Variables(변수)

변수 선언은 `@` 연산자를 사용 합니다. 변수에 값을 정의 함으로써 광범위 하게 사용 할수 있습니다.

{% codeblock lang:sass %}
// example.less

@color: #4D926F

#header {
  color: @color;
}
h2 {
  color: @color;
}
{% endcodeblock %}

`.css`로 변환 하면 `@color`의 값으로 치환됩니다.

{% codeblock lang:css %}
// compile.css

#header {
  color: #4D926F;
}
h2 {
  color: #4D926F;
}
{% endcodeblock %}
    
### Mixins(믹스 인)

믹스인은 클래스 처럼 사용 가능 하며 클래스에서 설정한 모든 속성을 포함 시킵니다. 또한, 함수와 같이 인수를 설정 할수 있습니다.

{% codeblock lang:sass %}
// example.less

.rounded-corners (@radius: 5px) {
  -webkit-border-radius: @radius;
  -moz-border-radius: @radius;
  -ms-border-radius: @radius;
  -o-border-radius: @radius;
  border-radius: @radius;
}

#header {
  .rounded-corners;
}
#footer {
  .rounded-corners(10px);
}
{% endcodeblock %}

`.rounded-coners`를 선언 하였고 기본 인수는 `@radius`는 `5px`입니다.
`#header`는 기본 인수를 사용 하였고 `#footer`는 사용자 인수를 사용해 `10px`이 되었습니다.

{% codeblock lang:css %}
// compile.css

.rounded-corners (@radius: 5px) {
  -webkit-border-radius: @radius;
  -moz-border-radius: @radius;
  -ms-border-radius: @radius;
  -o-border-radius: @radius;
  border-radius: @radius;
}

#header {
  -webkt-boder-radius: 5px;
  -moz-border-radius: 5px;
  -ms-border-radius: 5px;
  -o-border-radius: 5px;
  border-radius: 5px;
}
#footer {
  -webkit-border-radius: 10px;
  -moz-border-radius: 10px;
  -ms-border-radius: 10px;
  -o-border-radius: 10px;
  border-radius: 10px;
}
{% endcodeblock %}
    
### Nested Rules(중첩 규칙)

선택기를 중첩하여 상속 가능하므로 긴 이름의 선택기를 중복으로 사용하지 않고도 명확하고 짧게 사용할수 있습니다.

{% codeblock lang:sass %}
// example.less

#header {
  h1{
    font-size: 26px;
    font-weight: bold;
  }
  p {
    font-size: 12px;
    a {
      text-decoration: none;
      &:hover { border-width: 1px }
    }
  }
}
{% endcodeblock %}

`.less` 에서 한번 쓰인 `#heder` 선택기가 중복으로 적용됩니다.

{% codeblock lang:css %}
// compile.css

#header h1 {
  font-size: 26px;
  font-weight: bold;
}    
#header p {
  font-size: 12px;
}
#header p a {
  text-decoration: none;
}
#header p a:hover { border-width: 1px }
{% endcodeblock %}

### Functions & Operations(함수와 연산)

연산은 색이나 숫자에 대해 덧셈, 뺄셈, 나눗셈, 곱셈을 할수 있습니다. 속성 사이에 복잡한 연산은 CSS의 호환성을 위해
괄호 내에서만 실행 됩니다.

{% codeblock lang:sass %}
// example.less

@the-border: 1px;
@base-color: #111;
@red: #842210;

#header {
  color: @base-color * 3;
  border-left: @the-border;
  border-right: @the-border * 2;
}
#footer {
  color: @base-color + #003300;
  border-color: desaturate( @red, 10%);
}
{% endcodeblock %}

{% codeblock lang: css %}
// compile.css

#header {
  color: #333;
  border-left: 1px;
  border-right: 2px;
}    
#footer {
  color: #114411;
  border-color: #7d2717
}
{% endcodeblock %}
    
## The Language

### Variables(변수)

LESS에서 변수는 실제로 상수로 기억되며 변수는 오직 한번만 정의 됩니다.

`@nice-blue` 변수를 선언하고 + 연산을 합니다.

{% codeblock lang:sass %}
// example-01.less

@nice-blue: #5B83AD;
@light-blue: (@nice-blue + #111);

#header { color: @light-blue; }
{% endcodeblock %}
    
{% codeblock lang:css %}
// example-01.css

#header { color: #6c94be; }
{% endcodeblock %}

변수에 다른 변수를 정의 가능합니다.

{% codeblock lang:sass %}
// example-02.less
// @var에 문자열 'fnord'는 @fnord로 치환 됩니다.

@fnord: "I am fnord";
@var: 'fnord';
content: @@var;
{% endcodeblock %}

    
{% codeblock lang:css %}
// example-02.css

content: "I am fnord"
{% endcodeblock %}
    
### Mixins

Mixin은 이름을 사용해 선언 할수 있고 클래스 처럼 동작 합니다.

{% codeblock lang:sass %}
// example-03.less

.bordered {
  border-top: dotted 1px black;
  border-bottom: solid 2px black;
}
{% endcodeblock %}

클래스 이름을 사용해 속성을 포함 시킬수있습니다.

{% codeblock lang:sass %}
// example-03.less

.bordered {
  border-top: dotted 1px black;
  border-bottom: solid 2px black;
}

#menu a {
  color: #111;
  .bordered;
}
.post a {
  color: red;
  .bordered;
}
{% endcodeblock %}
    
선언된 `.bordered`는 `.css`에서 보이지 않으며 치환 된채로 컴파일 됩니다.
{% codeblock lang:css %}
// example-03.css

#menu a {
  color: #111;
  border-top: dotted 1px black;
  border-bottom: solid 2px black;
}
.post a {
  color: red;
  border-top: dotted 1px black;
  border-bottom: solid 2px black;
}
{% endcodeblock %}

### Mixins 인수 사용

클래스 처럼 믹스인 할수 있으며, 매개변수를 전달할수 있습니다.

{% codeblock lang:sass %}
// example-04.less

.border-radius (@radius) {
  border-radius: @radius;
  -moz-border-radius: @radius;
  -webkit-border-radius: @radius;
}

#header {
  .border-radius(4px);
}
.button {
  .border-radius(6px);
}
{% endcodeblock %}
    
`.button`의 `6px`, `#header`에 4px 값을 전달 받아 선언합니다.

{% codeblock lang:sass %}
// example-04.css

#header {
  border-radius: 4px;
  -moz-border-radius: 4px;
  -webkit-border-radius: 4px;
}
.button {
  border-radius: 6px;
  -moz-border-radius: 6px;
  -webkit-border-radius: 6px;
}
{% endcodeblock %}
        
매개 변수가 유효한 mixin은 기본값 `5px`을 가질수 있습니다

{% codeblock lang:sass %}
// example-05.less

.border-radius (@radius: 5px) {
  border-radius: @radius;
  -moz-border-radius: @radius;
  -webkit-border-radius: @radius;
}
#header {
  .border-radius;
}
{% endcodeblock %}
    
기본 인수로 치환된 `.css`

{% codeblock lang:css %}
// example-05.css

#header {
  border-radius: 5px;
  -moz-border-radius: 5px;
  -webkit-border-radius: 5px;
}
{% endcodeblock %}

정의된 선언 블록을 다른 규칙 세트에 이용하고 싶을때 정의된 규칙 세트 자체는
`.css`에 출력할 필요가 없을때 유용합니다.

{% codeblock lang:sass %}
// example-06.less

.wrap () {
    text-wrap: wrap;
    white-space: pre-wrap;
    white-space: -moz-pre-wrap;
    word-wrap: break-word;
}
pre { .wrap }
{% endcodeblock %}
    
{% codeblock lang: css %}
// example-06.css

pre {
  text-wrap: wrap;
  white-space: pre-wrap;
  white-space: -moz-pre-wrap;
  word-wrap: break-word;
}
{% endcodeblock %}
    
### The @arguments varialbe

`@arguments`를 사용해서 개별적으로 파라미터를 사용 하지 않아도 되며,
`@x`: `2px`, `@y`:`5px`와 같이 선언된 순서와 전달된 순서로 매치 됩니다.

{% codeblock lang:sass %}
// example-07.less

.box-shadow (@x: 0, @y: 0, @blur: 1px, @color: #000) {
  box-shadow: @arguments;
  -moz-box-shadow: @arguments;
  -webkit-box-shadow: @arguments;
}

.box-shadow(2px, 5px);
{% endcodeblock %}
    
0, 0값에서 전달된 2px, 5px값이 적용 됩니다.

{% codeblock lang:css %}
// example-07.css

.box-shadow: 2px 5px 1px #000;
-moz-box-shadow: 2px 5px 1px #000;
-webkit-box-shadow: 2px 5px 1px #000;
{% endcodeblock %}
    
## 패턴 매칭과 Guard 표현

### 기본 문법

mixin을 선언하고 조건문으로 인자를 비교해 같은 이름의 `.mixin`중에 참인 `.mixin`을 적용 합니다.

{% codeblock lang:sass %}
// basic-01.less

.mixin (@s, @color) {
    ….
}
.class {
  .mixin(@switch, #888);
}
{% endcodeblock %}
    
### 인수가 적용된 문법 표현

{% codeblock lang:sass %}
// basic-02.less

.mixin (dark, @color) {
  color: darken(@color, 10%);
}
.mixin (light, @color) {
  color: lighten(@color, 10%);
}
.mixin (@), @color) {
  display: block;
}
{% endcodeblock %}
    
### 패턴 매칭과 Guard 표현 사용법
`.mixin`이 3개가 선언 되었고 각기 다른 조건문을 가지고 있습니다.

{% codeblock lang:sass %}
// example-08.less

.mixin (dark, @color) {
  color: darken(@color, 10%);
}
.mixin (light, @color) {
  color: lighten(@color, 10%);
}
.mixin (@_, @color) {
  display: block;
}

@switch: light;
.class {
  .mixin(@switch, #888);
}
{% endcodeblock %}
    
호출시 조건문의 light값을 충족하며 모든 값을 의미 하는 `@_`포함 하여 적용 됩니다.

{% codeblock lang:css %}
// example-08.css

.class {
  color: #a2a2a2;
  display: black;
}
{% endcodeblock %}
    
### 인수의 개수검사

{% codeblock lang:sass %}
.mixin (@a) {
  color: @a;
}
.mixin (@a, @b) {
  color: fade(@a, @b);
}
{% endcodeblock %}
    
## Guards

가드는 값이나 변수의 개수가 아니라 식에 일치 시킵니다.
`if`/`else` 대신 `when`을 사용 합니다. `@a`값을 비교하여 적용 하며 인자가 하나이므로 `color`는 전체에 적용 됩니다.

{% codeblock lang:sass %}
// example-09.less

.mixin (@a) when (lightness(@a) >= 50%) {
  background-color: black;
}
.mixin (@a) when (lightness(@a) < 50%) {
  background-color: white;
}
.mixin (@a) {
  color: @a;
}
.class1 { .mixin(#ddd) }
.class2 { .mixin(#555) }
{% endcodeblock %}
   
조건에 따른 적용과 전체 적용된 `color`입니다.

{% codeblock lang:css %}
// example-09.css

.class1 {
  color: #ddd;
  background-color: black;
}
.class2 {
  color: #555;
  background-color: white;            
}
{% endcodeblock %}
    
### 가드 안에서 비교식(>, >=, =, =<, <)

두개의 식은 같은 표현 입니다.

{% codeblock lang:sass %}
// basic.less

.truth (@a) when (@a) { … }
.truth (@a) when (@a = true) { … }
{% endcodeblock %}
    
아래의 식은 위에 basic.less값에 매치 되지 않습니다. 값이 'true'만 매치 됩니다.

{% codeblock lang:css %}
// example-10.less

.class {
  .truth(40);
}
{% endcodeblock %}

### 조건문  

- = : 두 값이 같으면 참입니다.
- not : 두 값이 같지 않으면 참입니다.
- and : 모든 조건이 참이어야 합니다.
- ,   : 모든 조건 값중에 하나만 참이면 참입니다.

### JavaScript 'or'와 Less ','
JavaScript에서의 `or`와 같은 표현 조건중 하나만 참이어도 조건은 참입니다.
작성이 주의할점은 조건의 범위를 벗어난 값을 호출시 컴파일 자체가 되지 않습니다.

{% codeblock lang:sass %}
// example-11.less

.mixin (@a) when (@a > 10), (@a < -10) { … }
{% endcodeblock %}

### JavaScript 'and'와 Less 'and'

추가 조건문 and는 숫자인지 비교하고 0보다 높은 값이어야 합니다.

{% codeblock lang:sass %}
.mixin (@a) when (isnumber(@a)) and (@a > 0) { … }
{% endcodeblock %}

### 부정 조건문 not

0보다 크지 않을때 동작
{% codeblock lang:sass %}
.mixin (@b) when not (@b > 0) { … }
{% endcodeblock %}

### 인자비교및 대소 비교

{% codeblock lang:sass %}
// example-12.less

@media: mobile;

.mixin (@a) when (@media = mobile) { … }
.mixin (@a) when (@media = desktop) { … }

.max (@a, @b) when (@a > @b) { width: @a }
.max (@a, @b) when (@a < @b) { width: @b }
{% endcodeblock %}
    
### 매개변수 number, color등 확인

{% codeblock lang:sass %}
.mixin (@a, @b: 0) when (isnumber(@b)) { … }
.mixin (@a, @b: black) when (iscolor(@b)) { … }
{% endcodeblock %}
    
### 확인 가능한 is*형

- iscolor
- isnumber
- isstring
- iskeyword
- isurl
- ispixel
- ispercentage
- isem

## Nested 법칙

& 콤비네이터를 사용한 상속을 통해서 간결하게 만들수 있습니다. 아래는 .css파일 입니다. 이를 .less로 바꾸어 보겠습니다.

{% codeblock lang:css %}
// example-13.css

#header { color: black; }
#header .navigation {
  font-size: 12px;
}
#header .logo {
  width: 300px;
}
#header .logo:hover {
  text-decoration: none;
}
{% endcodeblock %}
    
.css에서 반복 되던 #header를 한번만 선언 할수 있습니다.

{% codeblock lang:sass %}
// example-13-01.less

#header {
  color: black;
  
  .navigation {
    font-size: 12px;
  }
  .logo {
    width: 300px;
    &:hover { text-decoration: none; }
  }
}
{% endcodeblock %}
    
위와 결과는 같지만 더 간결한 문법을 보입니다.
{% codeblock lang:sass %}
// example-13-02.less

#header { color: black;
  .navigation { font-size: 12px }
  .logo       { width: 300px;
    &:hover   { text-decoration: none }
  }  
}
{% endcodeblock %}

example-14.less

### & 콤비네이터 사용

{% codeblock lang:sass %}
// example-14.less

.bordered {
  &.float { flat: left; }
  .top {
    margin: 5px;
  }
}
{% endcodeblock %}
    
{% codeblock lang:css %}
// example-14.css

.bordered.float {
  flat: left;
}
.bordered.top {
  margin: 5px;
}
{% endcodeblock %}
    
### 향상된 & 사용법

`&` 또다른 사용 법입니다. 모든 셀렉터의 조합을 만들어 줄수 있습니다.

{% codeblock lang:sass %}
// example-15.less

.child, .sibling {
  .parent & {
    color: black;
  }
  & + & {
    color: red;
  }
}
{% endcodeblock %}
    
{% codeblock lang:css %}
// example-15.css

.parent.child, .parent.sibling {
  color: black;
}

.child + .child,
.child + .sibling,
.sibling + .child,
.sibling + .sibling {
  color: red;
}
{% endcodeblock %}
    
## 연산

숫자, 색, 변수를 연산 할수 있습니다.

{% codeblock lang:sass %}
// example-16.less

@base: 5%;
@filler: (@base * 2);
@other: (@bae + @filler);

color: (#888 / 4);
background-color: (@base-color + #111);
height: (100% / 2 + @filler);
{% endcodeblock %}
    
{% codeblock lang:sass %}
// example-16-01.less

@var: (1px + 5); // @var: 6px
{% endcodeblock %}
    
{% codeblock lang:sass %}
// example-16-02.less

width: ((@var + 5) * 2);
{% endcodeblock %}
    
## Color functions

### 밝기 조절

    lighten(@color, 10%);
    darken(@color, 10%);

### 채도 조절
    
    saturate(@color, 10%);
    desaturate(@color, 10%);
    
### 투명도
    
    fadein(@color, 10%);
    fadeout(@color, 10%);
    fade(@color, 50%);
    
### 색장 조절
    
    spin(@color, 10);
    spin(@color, -10);

### mix 사용법

`@color1`, 과 `@color2` 혼합된 값을 반환 합니다. `@weight`는 기본값 50%을 의미 합니다.

{% codeblock lang:sass %}
mix(@color1, @color2, @weight);
{% endcodeblock %}
    
### color luma 비교

`@color1` > 50% luma 일경우 `@darkcolor` 를 아니면 `@lightcolor`를 반환 합니다.

{% codeblock lang:sass %}
contrast(@color1, @darkcolor, @lightcolor;);
{% endcodeblock %}
    
### color 사용법
{% codeblock lang:sass %}
// exampl1-17.less

@base: #f04615;

.class {
  color: saturate(@base, 5%);
  background-color: spin(lighten(@base, 25%), 8);
}
{% endcodeblock %}
    
### color 정보 추출

{% codeblock lang:sass %}
hue(@color) // `@color` 색상 반환
saturation(@color) // `@color` 채도값 반환
lightness(@color) // `@color` 밝기값 반환
red(@color) // `@color` 'red'값 반환
green(@color) // `@color` `green`값 반환
blue(@color) // `@color` `blue`값 반환
alpha(@color) // `@color` `alpha`값 반환
luma(@color) // `@color` `luma`갑 반환
{% endcodeblock %}





    
### 새로운 색 구하기

`@new`는 `@old`의 색을 유지하면서 자신의 채도 및 밝기를 정의

{% codeblock lang:sass %}
@new: hsl(hue(@old), 45%, 90%);
{% endcodeblock %}
    
### Math functions

`1.67` 전달시 2를 반환 합니다

    round(1.67);
    
`2.4` 전달시 3을 반환 합니다.

    ceil(2.4);
    
`2.6` 전달시 '2'를 반환 합니다.

    floor(2.6);

퍼센티지 구하기

`0.5`전달시 50%를 반환 합니다.

    percentage(0.5)
    
### Namespaces

Namespace를 가지고 Mixin 에서 선택 할수 있습니다.
다음은 `#bundle` 에서 `.button`을 Mixin 하는 방법 입니다.

{% codeblock lang:sass %}
// example-18.less

#bundle {
  .button () {
    display: block;
    border: 1px solid black;
    background-color: grey;
    &:hover { background-color: white }
  }
  .tab { … }
  .citaion { … }
}

#header a {
  color: orange;
  #bundle > .button;
}
{% endcodeblock %}
    
`.tab`, `.citaion`은 적용 되지 않습니다.

{% codeblock lang:sass %}
// example-18.css

#header a {
  color: orange;
  display: black;
  border: 1px solid black;
  background-color: grey;
}
#header a:hover {
  background-color: #ffffff;
}
{% endcodeblock %}
    
### Scope

example-19.less

{ }안에서 변수 재선언시 지역적으로 사용 됩니다.
 
    @var: red;
    
    #page {
      @var: white;
      #header {
        color: @var;
      }
    }
    #footer {
      color: @var;
    }
    
### Comments

example-20.less

여러줄 주석 입니다. .css 변환시 에도 남아 있게 됩니다.

    /* Hello, I'm a CSS-style comment */
    .class { color: black }
    
example-21.less

한줄 주석입니다 .css변환시 보이지 않습니다.

    // Hi, I'm a silent comment, I won't show up in your CSS
    .class { color: white }
    
### Importing

example-22.less

기존에 만들어진 .less 파일과 .css 파일을 불러서 사용 할수 있습니다.

    @import "lib.less";
    @import "lib";
    
    @import "lib.css";
    
### String interpolation

example-23.less

문자열을 "" 안에 불러 올수 있습니다.

    @base-url: "http://assets.fnord.com";
    background-image: url("@{base-url}/images/bg.png");

### Selector Interpolation

example-25.less

셀렉터 이름도 불러 올수 있습니다.

    @name: blocked;
    .@{name} {
      color: black;
    }
    
example-25.css

    .blocked {
      color: black;
    }
    
### Escaping

example-24.less

    .class {
      filter: ~"ms:alwaysHasItsOwnSyntax.For.Stuff()";
    }
    
example-24.css

    .class {
      filter: ms:alwaysHasItsOwnSyntax.For.Stuff();
    }
        
### JavaScript evaluation

example-26.less

    @var: `"hello".toUpperCase() + '!'`;
    
compile

    @var: "HELLO!";
    
example-27.less

    @str: "hello";
    @var: ~`"@{str}".toUpperCase() + '!'`;
    
compile

    @var: HELLO!;
    
JavaScript환경에 액세스 할수 있습니다.

    @height:`document.body.clientHeight`;
