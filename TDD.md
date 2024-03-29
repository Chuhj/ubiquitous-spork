# TDD
JS는 잘못된 코드를 작성하기 쉽다.
예를 들어 ``` console.log = 1 ``` 라는 코드를 실행하면 아무 문제없이 실행된다.  
하지만 다음번에 console.log()를 실행하면 타입에러가 발생한다.  
이와 같이 JS는 빌드 과정이 없기 때문에 실행을 해야 문제를 발견할 수 있다.  

## 테스트 개념들
### 단위 테스트 (Unit Test)
* 단위: 특정 조건에서 어떻게 작동해야 할지 정의한 것. 대게 함수로 표현.  

준비(arrange), 실행(act), 단언(assert) 패턴을 따름.

### 테스트 주도 개발 (TDD)
TDD의 첫 번째 단계가 단위 테스트.
* 테스트 코드를 만듬.  
적색(기능 코드가 없어 테스트 실패) => 녹색(테스트 성공) => 리팩터(Blue)(코드 개선) 순환.  

이렇게 하면 테스트하기 쉬운 코드를 만들게 되고, 함수가 하나의 기능을 하게 만들게 된다.  
테스트 코드가 있기 때문에 안심하고 리팩토링을 할 수 있다.

## Jasmine 테스트 코드의 골격
```javascript
describe('hello world', ()=> { // 테스트 스윗: 테스트 유닛들의 모음 
  it('true is true', ()=> { // 테스트 유닛: 테스트 단위
    expect(true).toBe(true) // 매쳐: 검증자 
  })
})
```
* 테스트 꾸러미 (Test Suite)  
describe('테스트 설명', 테스트 구현 함수)  
* 테스트 스펙 (Test Spec)  
it('테스트 설명', 기대식을 가진 테스트 구현 함수)  
* 기대식과 매쳐  
expect(결과 값).toBe(기대하는 값)  
* 스파이  
spyOn(감시할 객체, 감시할 메소드)

## 테스트 할 수 없는 코드를 테스트하려면?
1. 코드를 UI에서 완전히 분리 - HTML에서 JS코드를 떼어내면 비즈니스 로직만 테스트 할 수 있음.
2. 자바스크립트를 별도 파일로 분리 - 다른 곳에서도 재사용. 테스트성도 좋아짐.

## 모듈 패턴
함수로 데이터를 감추고, 모듈 API를 담고 있는 객체를 반환하는 형태. (자바스크립트에서 가장 많이 사용하는 패턴)  
1. 임의 모듈 패턴 (임의 함수를 호출하여 생성하는 모듈 패턴)
```javascript
// 이름공간으로 활용한다.
var App = App || {};

// 이름공간에 함수를 추가한다. 의존성있는 God 함수를 주입한다.
App.Person = function (God) {
  var name = God.makeName();
  
  // API를 노출한다
  return {
    getName: function () { return name },
    setName: function (newName) { name = newName }
  };
}

const person = App.Person(God);
person.getName();
```
2. 즉시 실행 함수(IIFE) 기반의 모듈 패턴 (싱글톤 인스턴스가 됨)
```javascript
var App = App || {};
App.Person = (function () {
  let name = '';
  
  return {
    getName (God) {
      name = name || God.makeName();
      return name;
    },
    setName (newName) { name = newName } 
  }
})(); // 함수 선언 즉시 실행. 싱글톤

App.Person.getName(God);
```
### 모듈 생성 원칙
1. 단일 책임 원칙에 따라 모듈은 한 가지 역할만 한다.
2. 모듈 자신이 사용할 객체가 있다면 의존성 주입 형태로 제공한다. (또는 팩토리 주입)  
이렇게 하면 테스트하기 쉽다.  

## ClickCounter 예제
### ClickCounter
```javascript
describe('App.ClickCounter', ()=> {
  let counter;
  beforeEach(() => {
    counter = App.ClickCounter();
  })
  describe('getValue()', ()=> {
    it('초기값이 0인 카운터 값을 반환한다', ()=> {
      expect(counter.getValue()).toBe(0);
    })
  })

  describe('increase()', ()=> {
    it('카운터를 1 올린다', ()=> {
      const initialValue = counter.getValue();
      counter.increase();
      expect(counter.getValue()).toBe(initialValue + 1);
    })
  })
})
```
* beforeEach(): it 함수 호출 직전에 실행되는 jasmine 함수.  
중복되는 코드를 beforeEach로. DRY하게.  
### ClickCountView
#### updateView()
```javascript
// ClickCountView.js
App.ClickCountView = (clickCounter, updateEl) => {
  return {
    updateView() {
      const value = clickCounter.getValue();
      updateEl.innerHTML = value;
    }    
  }
}

// ClickCountView.spec.js
describe('App.ClickCountView', () => {
  let clickCounter, updateEl, view;
  beforeEach(() => {
    clickCounter = App.ClickCounter();
    updateEl = document.createElement('span');
    view = App.ClickCountView(clickCounter, updateEl);
  })
  describe('updateView()', () => {
    it('ClickCounter의 getValue() 값을 출력한다', () => {
      const value = clickCounter.getValue();
      view.updateView();
      expect(updateEl.innerHTML).toBe(value.toString());
    })
  })
})
```
#### ClickCountView에 의존성이 주입되었는지 체크
모듈을 사용하는 측에서 의존모듈을 넘겨주지 않으면 ClickCountView가 제대로 동작하지 않을 수 있다.
해당 테스트코드가 에러를 발생 시켜야 한다면 expect().toThrowError()를 사용한다.
```javascript
// ClickCountView.js 처음 부분에 추가
if (!clickCounter) {
  throw Error('no clickCounter');
}
if (!updateEl) {
  throw Error('no updateEl');
}

// ClickCountView.spec.js 'App.ClickCountView' 꾸러미에 추가
it('clickCounter가 주입되지 않으면 에러', () => {
  const clickCounter = null;
  const updateEl = document.createElement('span');

  const actual = () => App.ClickCountView(clickCounter, updateEl);
  expect(actual).toThrowError();
})

it('updateEl 주입되지 않으면 에러', () => {
  const clickCounter = App.ClickCounter();
  const updateEl = null;

  const actual = () => App.ClickCountView(clickCounter, updateEl);
  expect(actual).toThrowError();
})
```

## 테스트 더블
> 단위 테스트 패턴으로, 테스트하기 곤란한 컴포넌트를 대체하여 테스트하는 것
> 특정한 동작을 흉내만 낼뿐이지만 테스트 하기에는 적합하다.

다음 5가지를 통칭하여 테스트 더블이라고 함.  
* 더미(dummy): 인자를 채우기 위해 사용.
* 스텁(sturb): 더미를 개선하여 실제 동작하게끔 만든 것. 리턴값을 하드 코딩.
* 스파이(spy): 스텁과 유사. 내부적으로 기록을 남기는 추가기능.
* 페이크(fake): 스텁에서 발전한 실제 코드.
* 목(mock): 더미, 스텁, 스파이를 혼합한 형태.

자스민에서는 테스트 더블을 스파이스(spies)라고 부른다.  
spyOn(), createSpy()함수를 사용할 수 있다.  

```javascript
// clickCounter 모듈의 increase 함수를 감시하도록 설정한다.
spyOn(MyApp, 'foo')

// 특정 행동을 한 뒤
bar()

// 감시한 함수가 실행되었는지 체크한다.
expect(MyApp.foo).toHaveBeenCalled()

// bar()함수가 MyApp.foo()함수를 실행하는지 검증하는 코드이다.
```
