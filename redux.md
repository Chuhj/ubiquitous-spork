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
