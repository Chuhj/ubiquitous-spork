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
