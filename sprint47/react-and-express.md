#React & Express Webapp

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

