* Foo 객체 생성
```javascript
function Foo() {
    // 코드
}

Foo.prototype = {
    bar: function() {
        console.log('Foo_bar 실행');
    }
};
```
* Foo 함수의 prototype 속성은 프로토타입 객체를 참조
* 모든 객체가 프로토타입 객체 참조
* 프로토타입 객체의 생성자는 Foo 함수를 참조
* Foo 상속
```javascript
function Bar() {
}

Bar.prototype = Object.create(Foo.prototype);

Bar.prototype.baz = function() {
    console.log('Bar_baz 실행');
};

Foo.prototype.bar();
Bar.prototype.bar();
Bar.prototype.baz();
```

### Template Literal
* ``에 값을 넣어 사용
* ${변수명} 으로 사용가능
* 엔터로 줄바꿈가능
