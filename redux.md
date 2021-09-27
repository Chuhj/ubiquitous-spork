## Redux
* 단일 스토어
Redux is a state management library
1. Create Initial State
2. Define Action Types
3. Define Action Creators
4. Create Reducers
5. Change the initial State
6. Pass the parameters to the Creator function and the reducers

### Action
* action은 객체
  * { type: 'TEST' } payload 없는 액션
  * { type: 'TEST', params: 'hello' } payload 있는 액션
  * type만이 필수 property
* 액션을 생성하는 함수 = action creator(생성자)
  * 함수를 통해 액션을 생성해 액션 객체 리턴
```javascript
// 액션의 type 정의
const ADD_TODO = 'ADD_TODO';

// 액션 생성자
// 액션의 타입은 미리 정의한 타입을 가져와 사용
export function addTodo(text) {
  return { type: ADD_TODO, text };
}
```
### Reducer
* 액션을 주면 그 액션이 적용되어 달라진 결과를 만들어 줌
* 리듀서에서 모든 액션이 다 처리 가능해야 함
* state 한개만을 변경하는 액션들을 처리하는 리듀서 함수들을 따로 만들어 합침.
  * CombineReducers 함수로 합칠 수 있음.
* createStore(리듀서)함수로 스토어 생성
  * 스토어에 getState(), dispatch(), subscribe(), replaceReducer() 함수가 있음

### applyMiddleware
* 미들웨어를 적용하기 위한 함수.
```javascript
import { Provider } from 'react-redux';
import { createStore, applyMiddleware, compose } from 'redux';
import thunk from 'redux-thunk';
import promiseMiddleware from 'redux-promise';
import rootReducer from './_reducers/index';

const store = createStore(
  rootReducer,
  compose(
    applyMiddleware(promiseMiddleware, thunk),
    window.__REDUX_DEVTOOLS_EXTENSION__ && window.__REDUX_DEVTOOLS_EXTENSION__()
  )
);
// compose는 함수를 왼쪽에서 오른쪽으로 합쳐주는 함수.
// 미들웨어들을 다 적용하고 개발도구도 적용.
```
* 강의 내용
```javascript
const createStoreWithMiddleware = applyMiddleware(
  promiseMiddleware,
  reduxThunk
)(createStore);

createStoreWithMiddleware(reducer, window.__REDUX_DEVTOOLS_EXTENSION__ && window.__REDUX_DEVTOOLS_EXTENSION__())
```
* 이게 무슨 문법인가
