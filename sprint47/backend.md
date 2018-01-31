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



