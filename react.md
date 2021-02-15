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
