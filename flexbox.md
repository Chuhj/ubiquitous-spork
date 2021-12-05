# Flexbox
예전에는 레이아웃을 만들기 위해 position, float, table을 이용했다.
이것들로는 박스 안의 아이템들을 수직으로 가운데 정렬하는 것, 아이템들의 사이즈에 상관없이 동일한 간격, 사이즈로 박스 안에 배치하는 것, 박스를 동일한 높이로 두는 것 등을 하는데 제약사항이 있었다.
Flexbox로 위의 것들을 손쉽게 할 수 있다.

중요한 것!

* 첫 번째  
Flexbox는 container에 적용할 수 있는 속성 값, item들에 적용할 수 있는 속성 값이 존재한다.
* 두 번째  
Flexbox에는 중심축과 반대 축이 있다.
수평으로 정렬되어 있을 때, 수평축이 중심축, 수직축이 반대축이 된다.  

### Container
* display
* flex-direction
* flex-wrap
* flex-flow
* justify-content
* align-items
* align-content

### Item
* order
* flex-grow
* flex-shrink
* flex
* align-self

## Container
#### flex-direction
container에 display: flex; 를 지정하면 아이템들이 가로로 정렬될 건데, flex-direction 속성이 row로 기본 지정되어있기 때문이다.  
flex-direction 속성을 row-reverse로 지정하면 수평축을 중심축으로 반대쪽부터 반대 순서로 정렬된다.  
column이면 수직축을 중심축으로 item들이 정렬된다.  
column-reverse면 반대순서로 반대쪽부터 정렬된다.  

#### flex-wrap
기본값은 nowrap. 무조건 한 줄로 나열된다.  
wrap을 주면 한 줄이 다 찼을 경우 다음 줄로 넘어간다.  

#### flex-flow
flex-direction과 flex-wrap속성을 한 번에 설정할 수 있다.  
flex-flow: column wrap;  

#### justify-content
justify-content는 중심축에서 item들을 어떻게 배치할 것인지 결정한다.  
기본값은 flex-start. 왼쪽부터 item들을 배치한다.  
수직축이 중심축이라면 위부터 item들을 배치한다.  
flex-end는 flex-direction속성의 reverse와 다르게 item들의 순서를 유지한 채, 오른쪽 아래로 붙인다.
