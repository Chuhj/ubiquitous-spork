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

number는 64비트 부동소수점 방식을 사용. (메모리 최적화에 불리)  
연산 시 모든 값이 안전한 숫자여야 결과의 정확성이 보장된다. Number.isSafeInteger()  
Number.EPSILON - 매우 작은 값. 두 숫자의 차이와 EPSILON을 비교해 두 숫자가 비슷한지 판별.  

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
