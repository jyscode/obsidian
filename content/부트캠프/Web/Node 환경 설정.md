
 ### Router 사용

기존 Server.js 에서 라우팅을 전부 처리하는 로직을 사용하였다면, 도메인별로 나누어 보기 좋게 라우팅 작업을 수행할 수 있다.

`const router = require('express').Router()`

router는 실질적인 key, value를 저장하는 라우팅 역할을 하진 않는다, 실제 routing은 app이 수행

```js
router.get('/' , async (req, res) => {  
    try {  
        const {mongodb, mysqldb } = await setup()  
        res.send('HOME')  
    } catch (err) {  
        console.log(err)  
    }  
})

module.exports=router
```

라우팅을 작업 후 exports 해주면 server.js에서 가져와서 사용 가능하다.


`const accountRouter = require('./routes/account')`

export한 router 모듈을 가져온다.

`app.use('/account', accountRouter)`

미들웨어에 라우터를 등록하게 되면 첫번째 인자인 경로를 기준으로 새로운 라우팅을 할 수 있다.



### 환경변수 사용하기

nodejs에서는 보안에 취약한 변수들을 따로 관리하기 위한 dotenv모듈이 존재한다.

`npm i dotenv`

설정 방법은

1) .env 파일 생성 후 변수 저장, 키=값 형식
2) dotenv import -> require('dotenv').config()
3) 가져와서 사용하기 -> process.env.변수명

설정한 환경변수는 나중 github에 올릴 때 .gitignore파일에 .env파일을 등록하므로써 안전하게 사용가능하다.



---

### 로그인 상태별 동적 페이지


로그인, 로그아웃 버튼 전환

```
<span id="loginSpan">  
  <form action="/account/login" method="post">  
    ID <input size="3" name="userid">  
    PW <input size="3" name="userpw">  
    <input type="submit" value="login" class="btn btn-light">  
  </form></span>

...

const uid = $.cookie("uid");  
  
if (uid) {  
    $(".logined").removeClass("disabled");  
    $("#loginSpan").html(`${uid} <button onclick="logout()" class="btn btn-warning">logout</button>`);  
}

function logout() {  
    $.removeCookie("uid", { path: "/" });  
    location.href = "/account/logout";  
}
```

uid 존재 여부에 따라 span안의 내용을 동적으로 변경

로그아웃 버튼 클릭 시 Cookie 제거 후 session.destroy()를 실행하는 /account/logout으로 라우팅



### Postman 비정상 접속 차단하기

그냥 url 입력으로 /post/list에 접속하는 경우 동적 페이지 설정

`res.render("list.ejs", { data: result, user: req.session.user });`

Post에 session 값을 전달 후 검증

```
<% if (user) { %>

페이지

<% } else { %>
검증이 실패하였습니다.
<% } >
```



