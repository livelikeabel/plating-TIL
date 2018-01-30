# Redux

### redux 배경지식 | MVC, FLUX

**MVC**

Action -> controller -> model -> view

어떤 action이 입력되면, controller는 그 action을 받아서 model이 지니고 있는 데이터를 조회하거나 업데이트 할 수 있다. 그리고 그 변화는 view에 반영된다. 또한 view에서 model의 데이터에 접근하여 업데이트 할 수 있다.

**FLUX**

Action -> Dispatcher -> Store -> view

시스템에서 어떤 action을 받았을 때, dispatcher가 받은 action을 통제하여 store에 있는 데이터를 업데이트 한다. 그리고 변동된 데이터가 있으면, view에 리렌더링 한다. 그리고 view에서는 store에 접근하지 않는다.

view에서 dispatcher로 action을 보낸다. dispatcher에서는 작업이 중첩되지 않도록 해준다.(action을 대기시킴)

view -> action -> dispatcher -> store -> view

참고링크 : http://bestalign.github.io/2015/10/06/cartoon-guide-to-flux/

---

### redux 특징과 흐름

**redux :** flux 아키텍쳐를 좀 더 편하게 사용할 수 있게 해주는 라이브러리(즉, flux의 구현체)



#### **redux의 3가지 원칙**

1. **Single source of truth**

   어플리케이션의 state를 위해 단 한개의 store를 사용한다.

   > flux와의 주요 차이이다. flux에서는 여러개의 store를 사용한다.

2. **State is Read-only**

   어플리케이션에서 store의 state를 직접 변경할 수 없다.

   > state를 변경하기 위해선 무조건 **action**이 **dispatch** 되어야 한다.

3. **Changes are made with pure Functions**

   action 객체를 처리하는 함수를 reducer라고 부릅니다.

   reducer는 정보를 받아서 상태를 어떻게 업데이트 할 지 정의합니다.

   > **reducer는 '순수함수'로 작성되어야 합니다.**
   >
   > 즉, 네트워크 및 데이터베이스 접근 X, 인수 변경 X
   >
   > 같은 인수로 실행된 함수는 언제나 같은 결과를 반환
   >
   > '순수하지 않은' API사용불가(Date.now(), Math.random() 등)	



Redux 카툰 안내서 : http://bestalign.github.io/2015/10/26/cartoon-intro-to-redux/

-----

### Redux: 프로젝트 구조 및 컴포넌트 생성

```javascript
//value.js
//숫자를 보여주는 컴포넌트
import React from 'react';
import PropTypes from 'prop-types';

const propTypes = {
    number: PropTypes.number
};

const defaultProps = {
    number: -1
};

class Value extends React.Component {
    constructor(props) {
        super(props);
    }

    render() {
        return(
            <div>
              <h1>{this.props.number}</h1>
            </div>
        );
    }
}

Value.propTypes = propTypes;
Value.defaultProps = defaultProps;

export default Value;

```


```javascript
//control.js
//버튼3개를 보여주는 컴포넌트
import React from 'react';
import PropTypes from 'prop-types';

const propTypes = {
    onPlus: PropTypes.func,
    onSubtract: PropTypes.func,
    onRandomizeColor: PropTypes.func
};

function createWarning(funcName) {
    return () => console.warn(funcName + ' is not defined');
}
const defaultProps = {
    onPlus: createWarning('onPlus'),
    onSubtract: createWarning('onSubtract'),
    onRandomizeColor: createWarning('onRandomizeColor')
};

class Control extends React.Component {
    constructor(props) {
        super(props);
    }

    render() {
        return(
            <div>
              <button onClick={this.props.onPlus}>+</button>
              <button onClick={this.props.onSubtract}>-</button>
              <button onClick={this.props.onRandomizeColor}>Randomize Color</button>
            </div>
        );
    }
}

Control.propTypes = propTypes;
Control.defaultProps = defaultProps;

export default Control;
```


```javascript
//counter.js
//부모 컴포넌트(Smart Component)
import React from 'react';
import PropTypes from 'prop-types';

import Value from './Value';
import Control from './Control';

const propTypes = {

};
const defaultProps = {

};

class Counter extends React.Component {
    constructor(props) {
        super(props);
    }

    render() {
        return(
            <div>
                <Value/>
                <Control/>
            </div>
        );
    }
}

Counter.propTypes = propTypes;
Counter.defaultProps = defaultProps;

export default Counter;

```


```javascript
//app.js
import React from 'react'
import PropTypes from 'prop-types'
import Counter from './Counter';

const propTypes = {

};

const defaultProps = {

};

class App extends React.Component {

    constructor(props) {
        super(props);
    }

    render() {
        return(
            <Counter/>
        );
    }
}

App.propTypes = propTypes;
App.defaultProps = defaultProps;

export default App;
```

```javascript
//index.js
import React from 'react';
import ReactDOM from 'react-dom';

import App from './components/App';

ReactDOM.render(
    <App/>,
    document.getElementById('root')
);

```

----

### Action

**Action** : <u>작업에 대한 정보</u> 를 지니고 있는 **객체**

> miniproject에 필요한 action ( 대문자와 언더바를 사용함)
>
> 1.  값을 증가시키기
> 2. 값을 감소시키기
> 3. 새로운 색상 설정하기

Action 객체는 꼭 type을 가지고 있어야 한다.

{ type: "INCREMENT" }



```javascript
// actions/ActionTypes.js
export const INCREMENT = "INCREMENT";
export const DECREMENT = "DECREMENT";
export const SET_COLOR = "SET_COLOR";
```

```javascript
// actions/index.js
import * as types from './ActionTypes';

export function increment() {
    return {
        type: types.INCREMENT
    };
}

export function decrement() {
    return {
        type: types.DECREMENT
    };
}

export function setColor(color) {
    return {
        type: types.SET_COLOR,
        color: color
    }
}
```



----

### Reducer

**: 이전 상태와 액션을 받아서 다음 상태를 반환한다.**(previousState, action) => newState

​	<u>*이전 상태를 변경하는게 아닌, 새로운 상태를 반환하는 것이다.*</u> (기존 상태를 복사하고 변화를 준 다음에 반환)

- 변화를 일으키는 함수
- 순수해야함( 비동기 작업 x , 인수변경 x , 동일한 인수 = 동일한 결과)





```javascript
// reducers/counter.js

import * as types from '../actions/ActionTypes';

//초기 상태는 상수형태의 객체로 작성한다. //카운터에서 필요한 것은 숫자이다.
const initialState = {
    number: 0
};

//리듀서는 함수이다. export로 내보낸다.
export default function counter(state, action) {
    //이 함수가 처음 실행 될 때는 state가 undefined이다. 그럴땐 지정한 initialState를 반환해야한다.
    if(typeof state === 'undefined'){
        return initialState;
    }

    /*...*/

    return state;
}
```

es6 문법으로 아래와 같이 사용할 수 있다.

```javascript
// reducers/counter.js
//기본인수일때, state가 undefined일 때, initailState 할당
export default function counter(state = initialState, action) {
    /*...*/

    return state;
}
```



**Reduce 최종**

```javascript
//counter.js
import * as types from '../actions/ActionTypes';

//초기 상태는 상수형태의 객체로 작성한다. //카운터에서 필요한 것은 숫자이다.
const initialState = {
    number: 0,
    dummy: 'dumbdumb',
    dumbObject: {
        d: 0,
        u: 1,
        m: 2,
        b: 3
    }
};

//리듀서는 함수이다. export로 내보낸다.
export default function counter(state = initialState, action) {
    /*...*/
    switch(action.type) {
        case types.INCREMENT:
            return {
               ...state,
               number: state.number + 1,
               dumbObject: { ...state.dumbObject, u: 0}
            };
        case types.DECREMENT:
            return {
                ...state,
                number: state.number - 1
            };
        default:
            return state;
    }
}

```



```javascript
//ui.js
import * as types from '../actions/ActionTypes';

const initialState = {
    color: [255, 255, 255]
};

export default function ui(state = initialState, action) {
    if(action.type === types.SET_COLOR) {
        return {
            color: action.color
        };
    } else {
        return state;
    }
}
```



```javascript
//index.js

import { combineReducers } from 'redux';//redux에서 제공하는 combineReducers함수
import counter from './counter';
import ui from './ui';

const reducers = combineReducers({
    counter, ui
});


export default reducers;
```

----

### Store

어플리케이션의 현재 상태를 지니고 있음(리덕스를 사용하는 어플리케이션은 단 하나의 store를 가지고 있어야한다.)

```javascript
//index.js

import React from 'react';
import ReactDOM from 'react-dom';

import App from './components/App';

import { createStore } from 'redux';
import reducers from './reducers';

const store = createStore(reducers);

ReactDOM.render(
    <App/>,
    document.getElementById('root')
);
```



#### **store가 하는 일**

**dispatch(action)** : action을 reducer로 보낸다.

->  reducer가 어떤 변화가 필요한지 알아내서 변화를 주고, 새 상태를 주면 현 상태에 갈아끼운다.

**getState()** : 현재 상태를 반환하는 함수

**subscribe(listener)** : 상태가 바뀔 때마다 실행 할 함수를 등록하는 것이다. listener는 상태가 바뀔 때마다 실행될 콜백 함수이다.

**replaceReducer(nextReducer)** : hotreloading과 코드 분할을 구현할 때 사용함(보통 사용될 일 없음)

----

