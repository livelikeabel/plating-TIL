# Backend

### Node.js/express.js 맛보기 | 라우팅, 모듈화

#### 기본 라우팅

***app.METHOD(PATH, HANDLER)***

METHOD : HTTP 요청 메소드 - get, post, delete, put ….

PATH : 라우트 경로

HANDLER : 실행 될 콜백 함수

```Javascript
//javascript

var express = require('express');
var app = express();

app.get('/', function(req, res) {
    res.send('Hello World');
});

app.get('/user/:id', function(req, res) {
    res.send('Received a GET request, param:' + req.params.id);
});

app.post('/user', function(req, res) {
    res.send('Received a POST request');
});

app.put('/user', function(req, res) {
    res.send('Received a PUT request');
});

app.delete('/user', function(req, res) {
    res.send('Received a DELETE request');
});

app.listen(3000, function() {
    console.log('Example App is listening on port 3000');
});
```



#### Routes/user.js

> User 라우트 모듈화해서 내보내기

```javascript
//user.js
var express = require('express');
var router = express.Router();

router.get('/:id', function(req, res) {
    res.send('Received a GET request, param:' + req.params.id);
});

router.post('/', function(req, res) {
    res.send('Received a POST request');
});

router.put('/', function(req, res) {
    res.send('Received a PUT request');
});

router.delete('/', function(req, res) {
    res.send('Received a DELETE request');
});

module.exports = router;

```



#### main.js 

> 불러와서 사용하기

```javascript
var user = require('./routes/user');
/*...*/
app.use('/user', user);
```



```javascript
//main.js
var express = require('express');
var app = express();
var user = require('./routes/user');

app.get('/', function(req, res) {
    res.send('Hello World');
});

app.use('/user', user);

app.listen(3000, function() {
    console.log('Example App is listening on port 3000');
});
```



이렇게 모듈화를 하는 이유는 한 파일이 너무 커지게 되는 것을 방지하고, 코드를 나눔으로써 읽기도 간편해지고, 유지보수도 좀 더 편하게 하기 위해서 이다.

---

### Express | middleware

**middleware** : middleware함수는 요청 오브젝트(req), 응답 오브젝트(res), 그리고 애플리케이션의 요청-응답 주기 중 그 다음의 미들웨어 함수에 대한 액세스 권한을 갖는 함수입니다. (일종의 플러그인과 비슷)



미들웨어 직접 만들어보기(미들웨어도 콜백함수이다.)

```javascript
var myLogger = function (req, res, next) {
  console.log(req.url);
  next();
};

app.use(myLogger);
```

```javascript
//main.js
var express = require('express');
var app = express();
var user = require('./routes/user');

var myLogger = function(req, res, next) {
    console.log(req.url);
    next();
};

app.use(myLogger);

app.get('/', function(req, res) {
    res.send('Hello World');
});

app.use('/user', user);

app.listen(3000, function() {
    console.log('Example App is listening on port 3000');
});
```



Morgan: 로깅 미들웨어(terminal에 HTTP요청 메소드들 등 여러정보 보여준다.)

Body-parser: JSON 형태 데이터 파싱(json형태의 body를 읽게 해주는)



**routes/user.js**

> json 파싱하기

```javascript
router.post('/user', function(req,res) {
  console.log(JSON.stringify(req.body, null, 2));
  res.json({
    success: true,
    user: req.body.username
  })
});
```



**정적 (static) 파일 제공**

```javascript
app.use('/', express.static('public'));
```

