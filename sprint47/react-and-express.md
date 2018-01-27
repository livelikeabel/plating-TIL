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

### State

- component 에서 유동적인 데이터를 보여줄 때 사용된다.
- 사용할 때, 초기값 설정이 필수이다. 생성자(constructor)에서 this.state = { }으로 설정. // constructor의 parameter는 props이다..? - constructor가 만들어 질 때, 전달 받을것이다.
- 값을 수정 할 때에는 this.setState({…})을 통하여(component 내에서), 렌더링 된 다음엔 this.state = 절대 사용하지 말것.

```javascript
class Counter extends React.Component{
  //생성자메소드의 parameter는 props이다. Counter가 만들어질 때, 전달받을 props이다.
  constructor(props) {
    //super를 통하여 상속받은 클래스인 React.Component(즉 parents의 생성자 메소드를 먼저 실행하고, 우리가 할 작업들을 하는것이다. super(props)를 먼저 실행해주어야, 이 메소드 안에서 this.state라던지, props라던지를 접근할 수 있다.)
    super(props);
    this.state = {
      value: 0
    };
  }
  
  handleClick(){
    this.setState({
      value:this.state.value + 1
    });
  }
  
  render() {
    return(
      <div>
        <h2>{this.state.value}</h2>
        //this를 바인딩 해주어야함. handleClick에서 사용될 this는 render에서 사용되는 this와 같다.(bind(this)부분이 아직 잘 이해가 가진 않는다.)
        <button onClick={this.handleClick.bind(this)}>Press Me</button>
      </div>
    )
  }
}
```

-----

### Component Mapping

비슷한 코드를 반복해서 렌더링하는 방법...?

데이터 배열을 리액트에서 렌더링 할 땐 자바스크립트의 내장 함수인 map을 사용한다.

***Map() : parameter로 전달 된 함수를 통하여 배열 내의 각 요소를 처리해서 그 결과로 새로운 배열을 생성합니다.***

**arr.map(callback, [thisArg])**

callback : 새로운 배열의 요소를 생성하는 함수로서, 다음 세가지 인수를 가집니다.

​	currentValue : 현재 처리되고 있는 요소

​	index : 현재 처리되고 있는 요소의 index 값

​	array : 메소드가 불려진 배열

thisArg(선택항목) callback 함수 내부에서 사용 할 this 값을 설정

```javascript
ex)
let numbers = [1,2,3,4,5];

let result = numbers.map((num) => {
  return num*num;
});
//result = [1,4,9,16,25];
```

**잠깐 짚고가는 es6문법**

```javascript
//함수가 parameter가 1개 이고, 실행할 함수내부도 1줄일 때.
let one = a => console.log(a);  //es6

var one = function(a) {  //es5
  return console.log(a);
};

//parameter가 2개이고, 실행할 함수내부도 1줄일 때.
let two = (a,b) => console.log(a,b); //es6

var two = function(a,b){
  return console.log(a,b);
};

//함수의 내부가 여러개일 경우, bracket을 사용한다.
let three = (c,d) => { //es6
  console.log(c);
  console.log(d);
};

var three = function(c,d) { //es5
  console.log(c);
  console.log(d);
};
//parameter가 없을때
let four = () => {		//es6
  console.log('no params');
}

var four = function(){  //es5
  console.log('no params');
}
```



**Component mapping**

```javascript
class ContactInfo extends React.Component {
  render() {
    return( //props를 객체형식으로 받아와 사용하여 이름과 번호 렌더링
      <div>{this.props.contact.name}{this.props.contact.phone}</div>
    )
  }
}

class Contact extends React.Component {
  //state를 사용한다. 생성자 메소드에서 state를 초기화 한다.
  constructor(props) {
    super(props);
    this.state = {
      contactData: [
        {name:'Abel',phone:'010-0000-0001'},
        {name:'Betty',phone:'010-0000-0002'},
        {name:'Charlie',phone:'010-0000-0003'},
        {name:'David',phone:'010-0000-0004'}
      ]
    }
    
  }
  render() {
    //const : 변할일 없는 값을 선언할 때 사용
    const mapToComponent = (data) => {
      //contact는 data 배열의 각 데이터를 contact로 받아들이는 것, 그 데이터의 index를 i로 받아들임.
      return data.map((contact,i) => {
        //component를 리턴한다. key는 각 data의 식별자
        return(<ContactInfo contact={contact} key={i}/>);
      });
    };
    
    
    return(
      <div>
        {mapToComponent(this.state.contactData)}
      </div>
    );
  }
}

class App extends React.Component {
  render() {
    return (
      <Contact/>
    );
  }
};

ReactDOM.render(
  <App></App>,
  document.getElementById("root")
);
```





