
### Cookie

HTTP의 일종으로 사용자가 어떤 웹 사이트를 방문할 경우, 해당 사이트가 사용하고 있는 서버에서 **사용자의 컴퓨터에 저장하는 작은 기록 정보 파일**

쿠키는 클라이언트에서 수정할 수 있기 때문에 위변조의 위험이 항상 존재한다. 따라서 쿠키값(value)를 암호화해야 하며, 민감하거나 중요한 정보를 담지 않도록 해야한다.


### Session

일정 시간 동안 같은 사용자(브라우저)로부터 들어오는 일련의 요구를 하나의 상태로 보고, 그 상태를 유지시키는 기술이다.

사용 방법

`npm i express-session`


```js
let session = require('express-session')

app.use(session({
	secret: 'encryptstring'
	resave: false
	saveUninitialized: true
}))

// 세션을 사용할 수 있게 해주는 middleware
// saveUninitialized 세션에 저장할 내용이 없더라도 처음부터 생성할지 true 생성, false 저장할 내용 발생시 생성
```


세션에 데이터 넣기

`req.session.user = req.body`


세션 또한 탈취당할 위협이 존재함으로 로그아웃 기능 구현 필요

`req.session.destroy()`


---

### Session 을 사용한 유저 정보 표시


```js
// index.ejs

<% if(typeof user !='undefined' && user) { %>  
  <h3>반갑습니다 <%= user.userId%>님</h3>  
  <a href="/logout">로그아웃</a>  
<% } else { %>  
  <h3>로그인 해주세요</h3>  
  <p></p>  <a class="w-100 btn-warning login" href="/login"><b>로그인</b></a>  
  <a class="w-100 signup" href="/signup"><b>회원가입</b></a>  
<% } %>
```


### 비밀번호 암호화

보안을 위해 비밀번호를 암호화된 문장으로 바꾸어 저장해야 한다.

**Hash , Encryption**

Hash는 단방향 암호화 기법으로 복호화가 불가 SHA-256, SHA-512 권고
Encryption은 양방향 암호화 기법 복호화 가능

비밀번호를 Hash화 한 문자열로 저장 후, 비교할 때 입력값의 Hash한 값으로 저장된 문자열과 비교

```js
const crypto = require('crypto')


app.post('/signup', async (req, res) => {  
  
    req.body.userPw = crypto.createHash('sha256').update(req.body.userPw).digest('base64'),  
  
    await mydb.collection('account').insertOne(req.body)  
        .then(result => {  
            console.log('회원가입 성공')  
        })  
        .catch(err => {  
            console.log(err)  
        })  
  
    res.redirect('/')  
})

// 기존 userPw의 값을 sha256을 통한 Hashing된 userPw로 바꾸어 저장

```

