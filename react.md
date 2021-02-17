* react는 js로 구성
* 컴포넌트로 관리 => 독립적으로 기능, 재사용 가능
* 바뀔 여지가 있는 부분이 상태
* 컴포넌트의 render 부분에서 상태를 변경 setState
* Babel로 JSX (Javascript + XML) 사용가능 - script에서 태그들 사용가능
### 이전 state를 사용할 때 함수 사용
```javascript
this.setState((prevstate) => {
  return {
    value: prevstate.value + 1
  };
});
```
* DOM은 HTML 문서에 대한 인터페이스다. 뷰 포트에 무엇을 렌더링 할지 결정하기 위해 사용되며, 페이지의 콘텐츠 및 구조, 그리고 스타일이 자바스크립트 프로그램에 의해 수정되기 위해 사용됨
### DOM에 접근하기 위해 ref 태그에서 ref 사용
```javascript
<input ref={(c) => { this.input = c; }}>
```
