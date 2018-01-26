#React & Express Webapp

### ES6 클래스

- 컴포넌트는 그냥 자바스크립트 클래스 이다.(react 컴포넌트 class를 상속한다.)

```javascript
class Codelab extends React.Compenent {
  
}
```

- class는 es6에 새로 도입된 문법이다.

*클래스 선언 예.*

```javascript
class Polygon {
  //다른 언어가 그렇듯이, 생성자 메소드가 있다. 클래스가 새로 만들어 질 때, 실행되는 메소드.
  constructor(height, width){ 
    this.height = height;
    this.width = width;
  }
}
```

- js 클래스 안에서는 메소드만 만들 수 있다.
- 클래스를 사용할 때, 꼭 클래스를 먼저 선언해야한다.(클래스 선언전에 클래스를 사용하면 error)

아래의 스타일 처럼 만들 수 도 있다.

```javascript
//unnamed
var Polygon = class {
  constructor(height, width) {
    this.height = height;
    this.width = width;
  }
};

//named
var Polygon = class Polygon {
  constructor(height, width) {
    this.height = height;
    this.width = width;
  }
};
```

- 상속을 했을시, super키워드를 통해 부모 클래스를 호출 할 수 있다.

-----

### JSX의 특징

1. 모든  JSX형태의 코드는 container element 안에 포함 해주어야 한다.(container element가 없으면 error  발생)
2. JSX안에서 js를 표현하는 방법은 {}로 wrapping 하면 된다.

*Let : es6 문법. 블록 범위 내의 scope에서 변수를 선언하는 키워드. 한번 선언되면 다시 또 선언될 수 없다. (평상시에 let을 선언하도록 하자)*

3. JSX안에서 style을 설정할 때는 key가 camelCase인 객체가 사용되어야 한다.

```Javascript
render(){
  let style = {
    color: 'aquq',
    backgroundColor:'black' // camelCase사용해야함
  }
  
  return(
  	<div style={style}>React CodeLab</div>
  );
}
```

4. JSX안에서 주석을 작성할 때에는 {/\*.....\*/} 형식으로 작성해야 한다.(이 역시도 컨테이너 안에 있어야함)

---------

### Props

- 컴포넌트 내부의 immutable Data, 즉 변하지 않는 데이터를 처리할 때 사용된다.
- JSX 내부에 { this.props.propsName }
- 컴포넌트를 사용 할 때, <>괄호 안에 propsName = "value"
- this.props.children은 기본적으로 갖고있는 props로서, \<Cpnt>여기에 있는 값이 들어간다.\</Cpnt>



**기본값 설정**

컴포넌트 선언이 끝난 후, defaultProps 객체를 설정하면 된다.



**Type 검증**

특정 props 값이 특정 type이 아니거나, 필수 props인데 입력하지 않았을 경우 console에서 경고를 띄울 수 있다.

Type을 검증할 때는 컴포넌트의 선언이 끝난후, propTypes를 설정하면된다.(type종류는 많다. 리액트 메뉴얼을 보자)

proptypes를 지정하는 것은 필수가 아니다. 그러나 만든 컴포넌트가 제대로 사용되기 위해서, 유지보수를 위해서 설정하는 것이다.

------------



