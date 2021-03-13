## React
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
* 컴포넌트 분리 => 재사용성, 성능 최적화, 가독성
* jsx의 조건문은 삼항 연산자 사용
  
### 이전 state를 사용할 때 함수 사용
```javascript
this.setState((prevstate) => {
  return {
    value: prevstate.value + 1
  };
});
```
### Ref
```javascript
<input ref={(c) => { this.input = c; }}>
```
* DOM은 HTML 문서에 대한 인터페이스. 뷰 포트에 무엇을 렌더링 할지 결정하기 위해 사용되며, 페이지의 콘텐츠 및 구조, 그리고 스타일이 자바스크립트 프로그램에 의해 수정되기 위해 사용됨
* DOM에 접근하기 위해 ref 태그에서 ref 사용
* setState 실행 시 render 함수 실행
### useRef
* this의 속성을 Ref로 표현
* ref변수.current 로 사용
* 일반 값을 
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
```javascript
this.state.tries.map((v, i) => {
            return (
              <li key={v+1 유일한 값, 성능관리에 필요}>{v}</li>
            );
          });
```
* return 생략가능. v = value, i = index
### 컴포넌트로 props를 이용해 전달
```javascript
this.state.tries.map((v, i) => {
            return (
              <Try v={v} i={i}/>
            );
          });
```
```javascript
this.props.v, this.props.i 로 받음
```
### shouldComponentUpdate
```javascript
shouldComponentUpdate(nextProps, nextState, nextContext) {
  if (this.state.counter !== nextState.counter) {
    return true;
  }
  return false;
}
```
* 바뀌지 않는 부분은 렌더링 시키지 않기 위해 사용
* state가 바뀔때만 렌더링
* Component 대신 PureComponent 사용하면 자동으로 해줌.
* PureComponent
  * 배열과 객체를 새로 만들어야 바뀐걸 알아차림 - [...this.state.array, 1]
  * 컴포넌트가 복잡해지면 동작하지 않을 수 있음
* Memo(Hooks)
  * memo()로 감싸줌.
* 자식이 모두 PureComponent나 memo면 부모에게도 적용가능
### createRef
```javascript
class에서
inputRef = createRef();

this.inputRef.current.focus()
```
* Hooks에서는 current를 사용하였는데 class에서도 비슷하게 사용가능
### props 변경
```javascript
const [result, setResult] = useState(tryInfo);
or
state = {
  result: this.props.result,
};

const onClick = () => {
  setResult('1');
};
```
* props를 변경하고 싶을 땐, state를 새로 만들어 props를 넣어 변경.
### 클래스 라이프사이클
* constructor -> render -> ref -> componentDidMount -> (setState/props 바뀜) -> shouldComponentUpdate -> render -> componentDidUpdate -> componentWillUnmount
### componentDidMount()
* 컴포넌트의 render()가 처음 실행되고 나서 componentDidMount()가 실행
* 비동기 요청 많이 함
* 비동기 함수가 바깥 변수를 참조하면 클로저 발생
### componentDidUpdate()
* 리렌더링 후에 실행
### componentWillUnmount()
* 부모에 의해 컴포넌트가 제거되기 직전에 실행
* 비동기 요청 정리
### 메서드 호출하는 부분 간단하게하는 패턴
```javascript
onClickBtn = (choice) => () => {
}
//
onClick={this.onClickBtn}
```
### useEffect
```javascript
useEffect(() => { // componentDidMount, componentDidUpdate 역할
  interval.current = setInterval(changeHand, 100);
  return () => { // componentWillUnmount 역할
    clearInterval(interval.current)
  }
}, [imgCoord]);
```
* use Effect는 []안의 state가 변경 될 때 마다 실행
* componentDidUpdate()는 모든 state의 변경에 대해 실행
* 비동기로 바뀌는 state에서 뭔가 처리할 때 사용
### setInterval
* setInterval은 필요할 때 설정하고 componentWillUnmount() 에서 정리만 해주면 됨
### useMemo
* 복잡한 함수 결괏값을 기억
### useCallback
* 함수 자체를 기억, 그 함수 안의 상태 값은 초기값
* props로 전달하는 함수는 useCallback 써야함, 쓰지 않으면 props가 계속 바뀌는걸로 인식, 리렌더링
### useReducer
```javascript
const reducer = (state, action) => {
  switch (action.type) {
    case 'SET_WINNER':
      return {
        ...state,
        winner: action.winner,
      }
  }
};
const [state, dispatch] = useReducer(reducer, initialState);

const onClickTable = useCallback(() => {
    dispatch({type: SET_WINNER, winner: 'O'});
  }, []);
```
* state들을 줄일 수 있다.
* dispatch 안에 action 객체 dispatch로 action을 실행. 비동기.
* dispatch가 실행될 때 마다 reducer가 실행됨.
* action을 dispatch 해서 state를 바꾸는데 어떻게 바꿀지는 reducer에 있음
### Context API
* 값을 props로 계속 넘겨주는걸 대체해줌
* createContext와 useContext로 사용
* provider로 감싸서 값을 제공함
* useContext를 사용하면 전체가 리렌더링. => return 값을 useMemo로 캐싱해야함
  * return 부분을 컴포넌트로 분리해 memo도 사용가능
### React Router
* BrowserRouter과 HashRouter를 주로 씀
* 컴포넌트의 최상단을 Router로 묶어줘야함
* 컴포넌트들을 한번에 불러와 하나의 페이지에서 동시에 사용가능함
  * <Link to="/lotto-generator">로또</Link> // 공통인 부분
  * <Route path="/mine" component={Lotto} />
* 페이지가 실제로 여러개 존재 하는것이 아니고 눈속임일 뿐
* 
 
