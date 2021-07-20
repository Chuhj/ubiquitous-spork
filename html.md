## HTML, 태그

* \<h1> ~ \<h6> - 글자 크기 (숫자 클수록 작음)
* \<p> - 문단
* \<i> - italic
* \<sup> - 작은 글자
* \<ins> - 밑줄
* \<del> - 줄긋기

* \<a> - 하이퍼 링크
  * 속성의 target에 _blank는 새 창, _self는 현재 창
  
* \<dl> - 설명 목록
  * \<dt> - 설명할 요소
  * \<dd> - 설명
  
* \<table> - 표
  * \<tr> - row 행
  * \<td> - cell 열
  * 속성의 rowspan - 행 합침, colspan - 열 합침

* \<form action="" method="">
  * action - 폼 데이터가 도착할 URL
  * method - HTTP 메소드 결정 GET, POST

* html은 요소가 inline과 block으로 나뉨.
  * \<div>, \<li>, \<p> - block 요소
  * \<span> - inline 태그

## CSS
* tag, id, class 선택자 혼합
  * ul li.class
  
* 속성 선택자
  * input[type=text]
  
* 후손 선택자
  * 하위에 있는 모든 요소들 선택
  * div li
  
* 자손 선택자 ( > )
  * 바로 밑에있는 요소만 선택
  * div > li

* 동위 선택자 ( +, ~ )
  * \+ - 같은 레벨에 있는 요소 중 상위 한개만 선택
    * h3+div
  * ~ - 같은 레벨에 있는 요소 모두를 선택
    * h3~div
