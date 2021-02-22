* react는 js로 구성
* 컴포넌트로 관리 => 독립적으로 기능, 재사용 가능
* 바뀔 여지가 있는 부분이 상태
* 컴포넌트의 render 부분에서 상태를 변경 setState
* Babel로 JSX (Javascript + XML) 사용가능 - script에서 태그들 사용가능
* exports되는게 배열이나 객체면 구조분해 가능
  * //ES2015 문법
  * export const h = 'h' => import { h }
  * export defalut a => import a
  * //node.js(common.js) 문법
  * exports.h = 'h';
  * module.exports = a => require('a')
* input 태그의 value와 onChange는 세트. 사용안한다면 defaultValue 사용
  
### 이전 state를 사용할 때 함수 사용
```javascript
this.setState((prevstate) => {
  return {
    value: prevstate.value + 1
  };
});
```
* DOM은 HTML 문서에 대한 인터페이스. 뷰 포트에 무엇을 렌더링 할지 결정하기 위해 사용되며, 페이지의 콘텐츠 및 구조, 그리고 스타일이 자바스크립트 프로그램에 의해 수정되기 위해 사용됨
### DOM에 접근하기 위해 ref 태그에서 ref 사용
```javascript
<input ref={(c) => { this.input = c; }}>
```
* setState 실행 시 render 함수 실행
### Hooks 사용
```javascript
const [value, setValue] = React.useState('');
const inputRef = React.useRef(null);
setValue(value);
```
* Hooks로 setState 여러번 나와도 한번으로 처리 => 비동기이기 때문
* setState할 때 전체 함수를 다시 실행
* 태그 속성 class => className, for => htmlFor 로 사용
### Webpack
* webpack은 여러 파일을 하나의 js파일로 합쳐 html이 실행할 수 있게 만듬. 최신 문법을 엣날 브라우저에서도 돌아갈 수 있게 함 (babel?)
* @babel/preset-react => jsx 사용 가능
* @babel/preset-env => 옛날 브라우저에 맞춰줌
* preset은 플러그인 모음
* node.js로 돌리기 때문에 require 사용
### Hot reloading
* hot reloading - 기존 데이터 유지하면서 변경점이 있으면 리로딩
* react-refresh 와 @pmmmwh/react-refresh-webpack-plugin 설치 후 사용
* webpack-dev-server 설치
### 반복문 배열.map
'''javascript
this.state.tries.map((v, i) => {
            return (
              <li>{v}</li>
            );
          });
'''
* return 생략가능. v = value, i = index 
