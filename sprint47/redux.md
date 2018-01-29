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

