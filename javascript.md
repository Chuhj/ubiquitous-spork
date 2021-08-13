## JavaScript

### var
함수 스코프를 가짐.  
재정의 가능.  
for문, while문, if문 등에서 사용시 바깥에서도 var로 정의된 변수에 접근 가능.  

var로 정의된 변수는 변수가 속한 스코프의 최상단으로 끌어올려짐. - 호이스팅
호이스팅 된 후에 undefined가 할당됨.  
변수가 정의된 곳 위에서 값 할당 가능.  

### const, let
블록 스코프를 가짐.  
호이스팅이 된다. 하지만 아무 값도 들어가지 않아 사용하려고 하면 에러 발생.  
재할당 불가.  
객체의 속성은 변경 할 수 있다.  
let은 재할당 가능.

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
