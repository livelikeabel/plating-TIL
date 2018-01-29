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