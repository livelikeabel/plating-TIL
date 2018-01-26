####Object

-------------

**객체 생성자**

생성자는 객체를 만드는 방법 중 하나이다. 



일반적으로 객체를 생성할 때,

bob = new Object () 라고 작성할 때, Object라는 내장 생성자를 사용한다. (미리 정의되어 있는 생성자. 속성 x 메소드 x)



**Custom constructor**

ex)

```javascript
//java 처럼 미리 생성자를 만들어 놓을 수 있다.
function Person(name,age) {//생성자는 대문자로 시작하는게 관례인가?
  this.name = name;
  this.age = age;
}

// 작성한 생성자를 이용해서 우리의 친구 bob과 susan을 객체로 생성해 봅시다.
var bob = new Person("Bob Smith", 30);
var susan = new Person("Susan Jordan", 25);
// 이름이 "George Washington"이고 나이가 275인 객체 george 를 만드세요.
var george = new Person("George Wachington", 275);
```



생성자는 속성뿐 아니라 method도 가질 수 있다.



**Object의 Array**

ex)

```javascript
// Person 생성자:
function Person (name, age) {
    this.name = name;
    this.age = age;
}

// 이제, Person 객체로 이루어진 배열을 만들 수 있습니다.
var family = new Array();
family[0] = new Person("alice", 40);
family[1] = new Person("bob", 42);
family[2] = new Person("michelle", 8);
// 배열 family의 마지막 요소로, 6살 "timmy"를 추가하세요.
family[3] = new Person("timmy", 6);
```

























