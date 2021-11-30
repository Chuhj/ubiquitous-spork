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
1. 코드를 UI에서 완전히  - HTML에서 JS코드를 떼어내면 비즈니스 로직만 테스트 할 수 있음.
2. 자바스크립트를 별도 파일로 분리 - 다른 곳에서도 재사용. 테스트성도 좋아짐.

## 모듈 패턴
함수로 데이터를 감추고, 모듈 API를 담고 있는 객체를 반환하는 형태. (자바스크립트에서 가장 많이 사용하는 패턴)  
1. 임의 함수를 호출하여 생성하는 모듈
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
```
