## JavaScript

### var
함수 스코프를 가짐.  
재정의 가능.  
for문, while문, if문 등에서 사용시 바깥에서도 var로 정의된 변수에 접근 가능.  

var로 정의된 변수는 변수가 속한 스코프의 최상단으로 끌어올려짐. - 호이스팅
변수가 정의된 곳 위에서 값 할당 가능. - 호이스팅  
호이스팅 시 undefined가 할당됨.  

즉시 실행 함수로 스코프를 제한할 수 있다.
```javascript
(function () {
  for (var i = 0; i < 1; i++) {
    console.log(i);
  }
})();
console.log(i);
```

### const, let
블록 스코프를 가짐.  
호이스팅이 된다. 하지만 아무 값도 들어가지 않아 사용하려고 하면 에러 발생.  
재할당 불가.  
객체의 속성은 변경 할 수 있다.  
let은 재할당 가능.

### 호이스팅
어떤 변수나 함수의 선언부가 위치한 스코프의 최상단에서 해당 변수나 함수에 접근이 가능한 현상이다.
인터프리터가 변수와 함수의 메모리 공간을 선언 전에 미리 할당하는 것을 의미한다.
런타임에서는 변수와 함수의 선언이 스코프의 최상단으로 끌어올려진 것 처럼 동작하게 된다.

함수 선언식: 호이스팅되어 함수의 선언부 위에서도 실행 가능.
함수 표현식: 호이스팅 되지만 undefined로 초기화만 되어있음.

함수 호이스팅 → 변수 호이스팅
https://developer.mozilla.org/ko/docs/Glossary/Hoisting
https://tecoble.techcourse.co.kr/post/2021-04-25-hoisting/

### 기본 타입
number, bigint, string, boolean, object, symbol, undefined, null  
숫자가 아닌 문자열에 parseInt, parseFloat을 하면 NaN 반환.  
0으로 나눌 때 Infinity 반환.  
!!붙이면 boolean이 나옴.

#### Number
number는 64비트 부동소수점 방식을 사용. (메모리 최적화에 불리)  
연산 시 모든 값이 안전한 숫자여야 결과의 정확성이 보장된다. Number.isSafeInteger()  
Number.EPSILON - 매우 작은 값. 두 숫자의 차이와 EPSILON을 비교해 두 숫자가 비슷한지 판별.  

#### String
string은 불변.  
replace, replaceAll 함수로 변경된 문자열을 만들 수 있다.  
includes - 포함여부, startswith - 시작여부, endswith - 끝여부  
문자열 추출 - substr(시작 위치, 길이(없으면 끝까지)), slice(시작 위치, 끝 위치)  
문자열 위치 - indexOf, lastIndexOf  
문자열 분할 - split => 배열  
문자열 병합 - join => 문자열  
padStart, padEnd(길이, 문자) - 문자열 앞뒤에 넣어 길이를 맞춤.  

* tagged template literals 문법
```javascript
function taggedFunc(strings, ...expressions) {}
taggedFunc`a${b}c${d}`
// strings, expressions 각각에 배열로 값이 들어감.
// strings => ['a', 'c', '']
// expressions => [b에 해당하는 값, d에 해당하는 값]
```

* nullish coalescing
기본값을 지정하는 문법.
```const a = 'a' ?? '기본값'```  
이 경우 undefined 나 null일 경우 기본값을 사용하지만 0이나 빈 문자열에 대해서는 기본값을 사용하지 않음.  
따라서 0이나 빈 문자열에 대해서도 기본값을 사용하려면 ||을 이용하면 됨.

#### Object
중괄호, new 키워드, Object 생성자로 생성할 수 있음.  
delete 키워드로 속성을 삭제할 수 있음.  

#### Array
Array는 object 타입. 대괄호와 new 키워드로 생성 가능.  
map: 각 요소을 변경해 새로운 배열을 반환.  
reduce: acc와 요소들로 두 번쨰 인자부터 시작해 리듀서 함수를 실행해 하나의 결과값 반환.  
filter: 조건에 맞는 요소만 새로운 배열로 반환.  
반복문: for of, forEach  
splice: 배열의 원소를 삭제하면서 추가. (삭제 위치, 삭제 개수, ...넣을 원소)  

### 단축 속성명
객체의 속성에 변수만 넣으면 변수 이름이 속성 이름, 값에는 변수 값이 들어간다.  

### 계산된 속성명
객체의 속성명을 동적으로 결정.
속성의 key 부분에 대괄호로 변수를 속성의 이름으로 사용가능.  

### Spread operator
함수의 인자로 여러개를 넣을 때 사용가능.  
배열과 객체를 복사하거나 합칠 때 사용.  

### 비구조화
배열이나 객체의 요소들을 쉽게 꺼낼 수 있는 문법.  
```const [a,,c] = arr; // 쉼표로 값을 건너 뛸 수도 있다.```  
```const [first, ...rest] = arr; // rest에는 하나를 제외한 나머지 배열이 들어간다.```  
객체의 비구조화에서 기본값을 설정 가능한데, undefined인 경우에만 기본값 사용.  
기본값으로 함수의 반환값을 넣을 수 있다. 기본값을 사용할 때만 호출.  

### Optional Chaining
객체의 속성에 접근할 때 객체가 없으면 에러 발생.  
person?.name ?를 붙이면 검사를 해줌. 객체가 없다면 undefined.  
person.getName?.() 함수가 없다면 undefined.  
arr.[0] 배열에도 사용가능.  
nullish coalescing과 사용하기 좋음.  

### 일급함수
함수가 다른 변수처럼 취급되면 일급함수.  
자바스크립트는 함수를 변수에 담을 수 있다.  

### 클로저
함수와 그 함수를 둘러싼 주변의 상태를 기억하는 기능.  
내부함수가 외부함수의 지역변수와 매개변수에 접근 가능.  
자바스크립트는 함수의 지역, 매개변수가 함수가 실행된 후에도 존재.  

### 콜스택
함수의 실행정보를 관리하기 위해 사용.  
콜스택에 담기는 함수 실행 정보 - execution context  
프로그램이 처음 실행될 때 global execution context가 생성됨.  
execution context안에 lexical environment가 있음.  
lexical environment - 지역변수의 정보를 저장 - {변수이름:값}으로 이루어진 map이라 보면됨.  

### Execution context
실행 컨텍스트는 함수 실행에 대한 세부 정보를 담고 있는 내부 데이터 구조이다. 함수와 변수의 선언, 변수의 현재 값, this의 값, 상위 스코프 등 상세 내부 정보가 실행 컨텍스트에 저장된다.
Lexical environment와 VariableEnvironment로 구성되어 있다.

### Lexical environment
함수가 만들어질 때의 부모함수의 Lexical environment를 기억해두고 실행할 때 자신의 Lexical environment와 부모의 Le를 연결.  
함수 내부에서 함수가 만들어지면 Le는 유지됨.  

### 함수
매개변수의 기본값으로 함수를 설정하면 필수값으로 만들 수 있음.  
* named parameter: 매개변수를 중괄호로 감쌈. 함수를 사용할 때도 중괄호 사용. 매개변수의 이름을 명시. rest parameter 사용 가능.  
화살표 함수는 this와 arguments가 바인딩 되지 않음.  

### this
함수에서 사용가능.  
함수 내에서 화살표 함수로 정의하면 this는 함수가 생성될 당시의 this를 가리킴. 정적  
함수 내에서 일반 함수로 정의하면 this는 함수를 호출한 주체를 가리킴. 동적  

### Promise
콜백함수로 비동기 처리는 복잡함.  
* Promise란 비동기 상태를 값으로 다룰 수 있는 객체. 비동기 프로그래밍을 할 때 동기 프로그래밍 방식으로 코드 작성 가능.  
```javascript
const p = new Promise((resolve, reject) => {});
const p = Promise.resolve(param);
const p = Promise.reject('error message');
```
세 가지 방식으로 생성 가능하고 데이터를 가질 수 있다.  

* Promise 객체는 세 가지 상태를 가짐.  
* pending - 비동기 처리 중.
* fulfilled - 성공.
* rejected - 실패.
* fulfilled와 rejected를 settled라고 함. (다른 상태로 변할 수 없음)

비동기 처리가 끝난 후에 처리할 일을 then 메서드로 정의할 수 있다. fulfilled 상태면 첫 번째, rejected 상태면 두 번째 함수를 실행.  
then 메서드는 Promise 객체를 반환함. 다른 것을 반환하면 그것을 데이터로 하는 Promise 객체 반환.  
예외처리는 then, catch로 작성하는게 좋음. then에서의 예외도 잡힌다.  

* Promise.all([]) - 여러 Promise들을 병렬로 처리하고 싶을 때 사용.
하나라도 rejected 상태가 된다면 반환하는 객체도 rejected 상태.  
* Promise.race([]) - 가장 빨리 settled 된 Promise 객체를 반환.

### async await
비동기 프로그래밍을 할 때 동기 프로그래밍 방식으로 코드를 작성하는데 특화된 문법.  
async 함수 안에 await 오른쪽에 Promise 객체를 둘 수 있다. settled 상태가 될 때까지 기다림.  
병렬로 await를 사용하려면 Promise 객체를 먼저 생성하고 await 키워드를 사용. 또는 Promise.all()  
try catch문과 함께 사용하는게 좋음.  
* Thenable - Promise 처럼 동작하는 객체. then 메서드를 가짐.
  * async await 는 then 메서드를 가진 객체를 Promise 처럼 취급.

### 제너레이터
함수의 실행을 중간에 멈추고 재개할 수 있는 기능.  
yield로 값을 반환할 수 있음. 반환값: {value, done}, return 하면 done: true  
* next 메서드 - yield가 있는 곳 까지 실행 후 값 반환.
* return 메서드 - 멈췄던 곳에서 실행을 종료.
* throw 메서드 - 예외를 발생시킴.

제너레이터 객체는 iterable 하면서 iterator임.  
* iterator의 조건
  * next 메서드를 가짐.
  * next 메서드는 value와 done 속성값을 가진 객체를 반환.
  * done 속성값은 작업이 끝났을 때 참.

* iterable의 조건
  * Symbol.iterator 속성값으로 함수를 갖고있음.
  * 해당 함수를 호출하면 iterator를 반환.

for of 와 전개연산자 오른쪽에 iterable을 넣을 수 있음.

제너레이터 함수를 호출하면 실제로 실행되는게 아니고 제너레이터 객체만 생성.  
값이 필요한 순간에만 iterable을 통해 필요한 연산 수행 - lazy evaluate  

제너레이터 함수에서 다른 제너레이터 함수를 호출할 때는 yield* 키워드 사용. 키워드에 iterable 사용 가능.  

제너레이터 함수는 외부로부터 데이터를 받아 사용할 수 있음.  
next()에 값을 넣으면 현재 멈춰있는 yield의 반환값으로 쓰임.  

제너레이터 함수는 다른 함수와 협업 멀티태스킹(cooperative multitasking)을 할 수 있음. 실행을 멈추고 재개할 수 있기 때문.  
협업이 붙는 이유는 제너레이터가 실행을 멈추는 시점을 자발적으로 선택하기 때문.  

next() 부분에서 try catch문으로 예외처리.

### 프로토타입
Object.getPrototypeOf()로 프로토타입을 가져올 수 있음. (null 또는 object 타입) (\_\_proto\_\_ 속성으로 접근 가능)  
Object.setPrototypeOf()로 프로토타입을 변경할 수 있음.  

자기자신에 없는 속성이 있을 때 프로토타입에서 그 속성을 찾음.  
프로토타입을 여러 단계로 연결 가능.  

프로토타입은 일반적인 객체이기 때문에 함수를 정의해 공통로직을 추가할 수 있음.  

for in 을 사용하면 프로토타입에 있는 속성까지 순회.  
.hasOwnProperty() 메소드로 자기자신의 속성인지 확인 가능.  
Object.keys() 자기자신의 속성 반환.  

생성자 함수로 객체를 만들면 그 함수의 this를 반환함.  
함수는 먼저 this에 빈 객체 할당.

### 클래스
```javascript
class Person {
  constructor(name) {
    // 생성자
    this.name = name;
  }
}
```
클래스는 함수와 프로토타입을 기반으로 만들어짐.  
모든 함수는 프로토타입 객체를 가지는데 클래스에서 정의한 메소드들이 프로토타입 객체에 저장됨.  
멤버 변수는 각 객체에 할당됨.  

* 상속
```javascript
class Programmer extends Person {
  constructor(name, language) {
    super(name); // 부모의 생성자를 호출해야함
    this.language = language;
  }
}
```

```javascript
constructor(...args) {
  super(...args);
}
```
생성자를 정의하지 않으면 위의 생성자가 기본으로 사용.  
extends로 상속을 할 수 있음.  
자식 클래스의 객체는 부모 클래스의 메소드를 호출할 수 있음.  

클래스 상속도 프로토타입을 기반으로 구현.  
```javascript
console.log(Object.getPrototypeOf(Programmer.prototype) === Person.prototype);
console.log(Object.getPrototypeOf(Programmer) === Person);
```
자식 클래스의 프로토타입 객체는 부모 클래스의 프로토타입 객체를 프로토타입 체인으로 연결해서 갖고 있음.  
자식 클래스도 부모 클래스를 프로토타입 체인으로 연결해서 갖고 있음.  

* Class fields  
그냥 변수에 값을 등호로 넣으면 그 값은 프로토타입이 아니라 객체에 할당됨.  
부모에 Class fields와 자식에 이름이 같은 메서드가 있으면 객체에 있는것을 먼저 찾으므로 Class fields를 사용하게 됨.
클래스 필드와 화살표 함수를 같이 쓰면 콜백함수로 이 함수를 사용할 수 있음. 함수 안의 this는 문제없이 사용.  

super는 프로토타입을 기반으로 동작하기 때문에, 부모 클래스의 Class fields에 접근하려 하면 에러.  
super는 ```Programmer.prototype.__proto__.sayHello.call(this);``` 이런식으로 동작하는데 super를 사용한 메서드는 자기 자신의 클래스를 기억하고 있음. (HomeObject)  
자기 자신의 클래스를 기억하기 때문에 메소드를 추출해서 사용 가능. 

### document
* getElementById - Id에 맞는 요소를 찾아 반환.
* getElementsByClassName, Name, TagName - class, name, 태그 이름에 맞는 요소를 찾아 배열로 반환.
* querySelector - css selector 사용 가능. 선택자에 맞는 첫번째 하나의 요소 반환.
* querySelectorAll - 선택자에 맞는 모든 요소 배열로 반환.

요소의 className에 값을 넣으면 교체를 해버리므로 classList에 클래스 이름을 add, remove.  
이 기능을 classList.toggle()이 대신 함.

### Math
* Math.random() - 0과 1 사이의 랜덤한 숫자 반환.
* Math.floor() - 내림
* Math.ceil() - 올림
* Math.round() - 반올림

### JSON
* JSON.stringify() - js의 객체나 값을 JSON 문자열로 변환
* JSON.parse() - JSON 문자열을 객체로 변환
