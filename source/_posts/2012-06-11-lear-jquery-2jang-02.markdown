---
layout: post
title: "Lear jQuery 2장-02"
date: 2012-06-11 14:26
comments: true
categories: Learn jQuery
---

Source
------

[예제.html](https://gist.github.com/2908591)

[예제 css ]( https://gist.github.com/2908588)

[예제 js  ](https://gist.github.com/2908628)

본문 - 테이블행에 징검다리 색깔 입히기
----

## 사용자 정의 선택자

class명 horizontal를 가진 div 집합의 두번째 항목 선택
$('div.horizontal:eq(1)')
두번째 항목이 1인 이유는 자바스크립트 배열에서 인덱스는
0에서 부터 시작 하며 jQuery또한 마찬가지이다.
단, css는 1을 기반으로 한다.

헤더 행 스타일 입히기

    $('th').addClass('table-heading');
    //<th class=table-heading'>

odd,even 색 입히기

    $('tr:not(:has(th)):even').addClass('even');
    $('tr:not(:has(th)):odd').addClass('odd');
    //odd와 even의 색 정의는 css에 정의 되어있다.

테이블에서 특정단어 포함 셀만 강조

    $('td:contains("Henry")').addClass('highlight');
    //td에 Henry 단어가 포함 된열 강조
    // highlight의 색 정의는 .css에 정의 되어있다.

Henry를 포함한 셀을 찾아낸후 모든 하위레벨에 클래스 추가

    $('td:contains("Henry")').siblings().addClass('highlight');

Henry를 포함한 부모를 찾아 인덱스가 0보다 큰셀들을(0은 최상 부모) 순회하면 클래스추가 

    $('td:contains("Henry")').parent().find('td:gt(0)').addClass('highlight');

Henry를 포함한 셀을 찾아 부모를 찾고 그 안의 모든 셀을 찾은후 Henry를 포함한 셀을
필터링한후 클래스추가(Henry만 적용을 하지 않음)

    $('td:contains("Henry")').parent().find('td').not(':contains('Henry")')).addClass('highlight');

Henry를 포함하고 있는 셀을 찾아낸 후에 그것의 부모를 얻어와서 자식들 중에 두번째 셀을
찾아서 클래스를 추가하고 가장 최근의 .find()를 취소한 후에 다시 자식들 중에서 세 번째 셀을
찾아서 클래스를 추가한다.

    $('td:contains("Henry")') //Henry셀을 찾고
    .parent()  //부모를 찾아서
    .find('td:eq(1)') //부모의 두번째 셀을 찾아
    .addClass('highlight') //강조 하고(클래스 추가)
    .end() // 다시 부모로 돌아와
    .find('td:eq(2)') // 세번째를 찾아서
    .addClass('highlight'); //강조 한다(클래스 추가)

Command Action
------

**addClass(names)**

매개변수로 전달된 하나 이상되는 클래스명을 확장 집합의 모든 엘리먼트에 추가한다.

**매개변수**

names (String)클래스명을 포함 하는 문자열, 여러 클래스명을 추가할 때는 공백으로 구분

반환값 - 확장집합

---------------------------

**removeClass(names)**

매개변수로 전달된 하나 이상되는 클래스명을 확장 집합의 모든 엘리먼트에서 삭제한다.

**매개변수**

names (String)클래스명을 포함 하는 문자열, 여러 클래스명을 추가할 때는 공백으로 구분

**반환값**

확장집합

----------------------

**siblings()**

확장 엘리먼트의 모든 형제를포함 하는 확장 집합을 반환

------------------------

**find(selector)**

  원본의 모든 엘리먼트 중 전달된 셀렉터 표현식과 일치하는 엘리먼트로 구성된 새로운 확장 집합
  을 반환한다. 확장 집합에 포함된 엘리먼트의 자손 엘리먼트도 전달된 표현식과 일치하는지 평가

**매개변수**

selector (String) 반환될 집합의 일부가 될 엘리먼트가 일치하는 셀렉터

**반환값**

새로 생성된 확장 집합

변수 wrappedSet에 할당된 확장 집합에서 p문단 인용문(&gt;cite&lt; 엘리먼트)로 구성된 확장 집합은
두가지로 표현 된다

    wrappedSet.find('p cite')
    $('p cite', wrappedSet)

--------------------------

**parent()**

  확장 집합 내에 있는 모든 확장 엘리먼트의 바로 위 부모로 구성된 확장 집합을 반환한다.

**parents()**

  모든 확장 엘리먼트의 조상으로 구성된 확장 집합을 반환한다. 바로 위 부모와
  상위의 모든 소상이 포함 되지만 문서 루트(document root)는 포함 되지 않는다(?)

--------------------------

**end()**

  jQuery 커맨드 체인에서 사용하며 이전 확장 집합으로 돌아간다.

**매개변수**

  없음

**반환값**

이전 확장 집합
