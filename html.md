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

### 선택자
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

* 반응 선택자
  * 마우스의 반응에 따른 속성을 설정
  * :hover - 마우스를 올렸을 때의 요소

* 상태 선택자
  * 상태에 따른 속성을 설정
  * :focus - form의 input 태그 등 포커스를 받았을 때 속성을 설정
  * :enabled - 모든 활성 요소 (input, button...)
    * 활성 요소란 활성(선택, 클릭, 입력 등등)하거나 포커스를 받을 수 있는 요소를 말함
  * :disabled - 비활성 되어있는 요소 (disabled 속성을 가진 input)

* 구조 선택자
  * 구조에 따른 속성을 설정
  * :first-child - 형제 요소 중 제일 첫 요소
  * :last-child - 형제 요소 중 제일 마지막 요소
  * :nth-child() - 괄호 안에 n을 활용하여 인덱스 지정 가능.
    * 홀수 (2n + 1)
    * 짝수 (2n)

* 문자 선택자
  * 특정 문자 또는 문자열을 선택하여 속성을 설정
  * ::first-letter - 첫 번째 글자
  * ::first-line - 첫 번째 줄
  * ::selection - 드래그 되어있는 문자들

* 링크 선택자
  * 링크되어 있는 요소를 선택
  * a::after { content: '-' attr(href) }
  * 문자 - href값
  
* 부정 선택자
  * 선택한 요소를 제외한 모든 요소를 선택
  * :not - 선택한 요소를 제외한 요소

### 속성
* 단위
  * px
  * %
  * em - 기본 1.0 (16px 정도)  
    해당 요소의 font-size를 1em, 없다면 부모 요소의 font-size를 1em으로 사용.
  * rem - html의 font-size를 1rem으로 사용

* url 함수
  * background-img 속성의 속성값으로 많이 사용됨. 이 경우 배경 이미지의 경로
  * background-img: url('');

* display 속성
  * 요소가 화면에 어떻게 보이는지를 설정
  * block - 자동으로 새로운 라인에서 시작함. 해당 라인의 모든 너비를 차지
  * inline - 같은 라인에서 시작함. height 속성 적용 안됨
  * block-inline - 같은라인에서 시작하고, height 속성 적용 가능
  * none - 요소가 안보임. 영역을 차지 안함.

* visibility 속성
  * hidden - 영역을 차지 하지만 보이지 않음

* opacity 속성
  * 기본 1.0
  * 줄이면 투명해짐

* margin 속성
  * 요소의 바깥쪽 여백을 설정
  * 위 - 오른쪽 - 아래 - 왼쪽
  * 위 - 양옆 - 아래
  * 위아래 - 양옆

* padding 속성
  * 요소의 안쪽 여백을 설정
  * 내용과 테두리 사이의 여백
  * background를 확장시킴

* box-sizing 속성
  * border-box - border가 안쪽으로 만들어짐

* border 속성
  * 테두리를 설정함
  * border-width, border-style, border-color 순으로 값을 설정
  * 3가지 속성을 따로 설정 가능

* background 속성
  * background-img - url함수로 이미지 지정 가능
  * background-size - 기본 100%. 줄이면 이미지가 반복되어 나옴.
  * background-repeat - no-repeat 설정하면 한번만 나옴.
  * background-attachment - fixed 설정하면 이미지가 브라우저의 왼쪽상단부터 있다고 가정하고 나타남. 뷰포트에 고정

* font-family 속성
  * 글꼴 설정

* font-size 속성
  * 폰트 크기 설정

* font-style 속성
  * 폰트 스타일 설정 (italic)

* font-weight 속성
  * 폰트의 가중치나 굵기를 설정 (normal, bold, boler, lighter)

* line-height 속성
  * 행간격 설정
  * 부모의 height와 같게 설정하면 위아래 정렬 가능

* text-align 속성
  * 가로 정렬을 설정 (center)

* text-decoration 속성
  * 글씨를 장식 (underline, overline, line-through, none)

* position 속성
  * 기본 static
  * absolute - position: static 속성을 가지고 있지 않은 부모를 기준으로 위치를 설정. 없으면 body 기준
  * relative - 부모를 기준으로 위치를 설정
  * fixed - 스크롤을 내려도 브라우저에서 위치를 고정시킴
