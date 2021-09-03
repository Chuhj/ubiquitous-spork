# Nodejs
* Node.js 는 서버사이드 자바스크립트이며 구글의 자바스크립트 엔진인 V8을 기반으로 구성된 일종의 소프트웨어 시스템이다.
* 이벤트 기반으로 개발이 가능하며 Non-Blocking I/O를 지원하기 때문에 비동기식 프로그래밍이 가능하다.
* 콘솔에서 입력값 받기 process.argv

## Body-parser
요청의 body를 해석하는 미들웨어.  
```javascript
app.use(bodyParser.urlencoded({ extended: true }));
app.use(bodyParser.json());
```
노드 4.16 버전 이후로는 내장되어 있는 함수 사용.  

bodyParser.json()은 'application/json' 방식의 Content-Type 데이터를 받음.  
bodyParser.text()은 'text/xml' 방식의 Content-Type 데이터를 받음.  
bodyParser.urlencoded({})은 'application/x-www-form-urlencoded' 방식의 Content-Type 데이터를 받음.  

extended 옵션을 false로 하면 querystring, true로 하면 qs 라이브러리를 사용하여 url-encoded data를 파싱함.  
qs 라이브러리는 중첩된 객체도 파싱. 깊이는 5까지 가능.  

## Util 모듈
* util.format(format, [...]) : console.log() 메소드와 비슷한 기능이지만 console.log()는 화면에 출력하고 util.format은 문자열로 반환합니다.  
%s : 문자열  
%d : 숫자(정수부터 소수까지 표현 가능)  
%j : JSON  

* util.debug(string) : 프로그램의 실행을 멈추고 즉각적으로 string을 출력합니다.
* util.log(string) : 타임스탬프 시간과 함께 string을 출력합니다.
* util.isArray(object) : 주어진 object가 Array이면 true, 아니면 false를 리턴합니다.
* util.isRegExp(object) : 주어진 object가 RegExp이면 true, 아니면 false를 리턴합니다.
* util.isDate(object) : 주어진 object가 Date이면 true, 아니면 false를 리턴합니다.
* util.isError(object) : 주어진 object가 Error이면 true, 아니면 false를 리턴합니다.

## 상속
### util.inherits()를 이용한 상속
```javascript
var util = require('util');

function Bar() {
}

util.inherits(Bar, Foo);

Bar.prototype.baz = function() {
	console.log('Bar_baz 실행');
};

Foo.prototype.bar();
Bar.prototype.bar();
Bar.prototype.baz();
```

## Pug
```pug
html
    head
    body
```
* 인덴트로 계층구조 표현
```pug
html
    head
    body
    div#goormDiv1
    div#goormDiv2.divStyle1
```
* #으로 id, .으로 class 표현
* div 생략하면 div로 인식
```pug
#contents(style="border:1px solid black;")
    input(type="checkbox", checked)
```
* 괄호로 나머지 속성 표현
* |로 아래줄 이어적기 가능

## socket.io
```javascript
var io = require('socket.io').listen(app);
io.on('connection', function (socket) {
```
* connection 이벤트는 사용자가 웹사이트를 들어오면 자동 발생
* 사용자의 socket이 함수의 파라미터로 전달됨
* socket.on으로 이벤트를 받고 socket.emit으로 이벤트 발생 io.emit은 접속한 클라이언트 모두에게

## Query string
* require("url")
* url.parse("url", true).query => {a: 1, b: 2} 반환
