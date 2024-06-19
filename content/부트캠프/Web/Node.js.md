
V8 엔진을 탑재한 크롬브라우저의 빠른 성능이 입증되자 웹 브라우저가 아닌 곳에서도 javascript를 사용하고 싶었는데 , 이로 인해 생긴게 node.js 이다.

 ```
docker run --name some-postgres -e POSTGRES_PASSWORD=password -p 5432:5432 -d 
```


### Express

Node.js로 웹서버를 쉽게 만들기 위해 도와주는 도구

```js
// express가 해당 경로로의 요청을 뺏어가지 않고 직접 접근할 수 있게 해줌
app.use(express.static('public'))


app.get('/', (req, res) => {})
app.listen(3000, function(){

})
```


---

## DB 연결


### MySQL

설치하기(docker)

MariaDB 유저 생성 및 비밀번호 지정, MARIADB_ROOT_PASSWORD 필수
```zsh

docker run --detach --name db -e MARIADB_USER=jyscode -e MARIADB_PASSWORD=password -e MARIADB_DATABASE=exmple-database -e MARIADB_ROOT_PASSWORD=password  -p 3306:3306 mariadb:latest


# 생성 확인
docker ps -A | grep db

```

접속 Terminal 또는 Mysqlworkbench

```zsh
mariadb -uroot -h 127.0.0.1 -p
```

명령어들

```
# 데이터 베이스 조회
show databases;

# 데이터 베이스 생성
create database myboard default character set utf8;

# 데이터 베이스 사용 (이름 myboard)
use myboard;

# 테이블 조회
show tables;

# 테이블 생성
create table post(
	id int,
	...
);


# 데이터 추가
insert into post (title, content, created, writer, email) values('삶은', '계란이다', NOW(), 'lee', 'lee@naver.com');


# user 권한 추가 (root 계정에서)
grant all privileges on *.* to 'jyscode'@'%';

```

**Node와 연결하기**

mysql 디펜던시 추가
`npm i mysql2`

```js
const mysql = require('mysql2')  

// 연결하기
const conn = mysql.createConnection({  
    host: 'localhost',  
    user: 'jyscode',  
    password: 'password',  
    database: 'myboard'  
})

app.get('/list_mysql', async function(req, res) {  
    try{ 
    // 연결 생성 
        conn.connect()
		// 데이터를 담고 있는 rows와 table의 구조를 가지고 있는 fields 
        let [rows, fields] = await conn.promise().query('select * from post join profile on post.profile_id = profile.id')  
        console.log(rows)  
        res.render('list_mysql.ejs', {data: rows})  
    } catch (e) {  
        console.log(e)  
    }  
  
})



```

### MongoDB

NoSQL로 RDBMS 보다 유연하여 데이터의 구조를 알  수 없거나 변경해야 하는 경우 사용하게 된다.
MongoDB는 설치형과 Cloud 버전이 있는데 Cloud 형태로 사용하려면 Atlas를 사용하면 된다.


설치하기

MongoDB Cloud인 Atlas 홈페이지에 접속

New Project - 새로운 프로젝트 생성
Database Access - Admin 권한을 가지는 계정 생성
Database -> connect - Node JS와 연결하는 url 복사
Databases -> Browse Collections - DB와 테이블 생성 가능, 데이터 추가 가능




**NodeJS와 연결**

디펜던시 추가
`npm i mongodb`

```js

const mongoClient = require('mongodb').MongoClient  
const url = '개인 URL 사용'  
let mydb  
mongoClient.connect(url)  
    .then(client => {  
        console.log('mongodb에 접속 성공')  
        mydb = client.db('myboard')  
        app.listen(8080, function (){  
            console.log('8080 server ready...')  
        })  
  
    }).catch(err => {  
        console.log(err)  
    })

app.get('/list', function(req, res) {  
    mydb.collection('post').find().toArray().then(result => {  
        console.log(result)  
        res.render('list.ejs', {data: result})  
        //res.sendFile(__dirname+ '/list.ejs')  
    })  
})
```










---


### Modal 

동적인 상황에서는 script로 띄우는 것이 유리


---

### Data 전송

form tag를 사용하면 입력값을 전달할 수 있다.

```
// save로 param1이라는 이름을 가진 입력 데이터 전송
<form action='/save'. method='post'>
	<input type='text' name='param1'/>
</form>
```




app.post('/save') 경로의 req.body에 title과 content라는 input값을 보낸다.

```html
<form action="/save" method="post">  
    <div class="mb-3">  
        <label for="exampleFormControlInput1" class="form-label">제목</label>  
        <input type="text" name="title" class="form-control" id="exampleFormControlInput1">  
    </div>    <div class="mb-3">  
        <label for="exampleFormControlTextarea1" class="form-label">내용</label>  
        <textarea class="form-control" name="content" id="exampleFormControlTextarea1" rows="3"></textarea>  
    </div>    <button type="submit">저장</button>  
</form>
```

req.body값을 간단히 얻기 위한 body-parser 설치
express 를 사용하는 경우 설치 불필요 (내장 되어 있음)

```js
// form 같은 데이터 처리
app.use(express.urlencoded({ extended: true }));  

// json 형식의 데이터 처리
app.use(express.json());
```




```js
app.post('/save', function (req, res){  

	// 객체 형식으로 저장됨
    const body = req.body  

	// 객체 저장 
    mydb.collection('post').insertOne(body).then(result => {  
        console.log('저장 완료')  
    })  
  
    console.log(body.title)  
    console.log(body.content)  
})


// MySQL version
app.post('/save_mysql', async function (req, res){  
    try{  
        const body = req.body  
        conn.connect()  
        let result = await conn.promise().query("insert into post (title, content, created, profile_id) values(?, ?, NOW(),?)", [body.title,  
        body.content,  
        body.profile_id])  
        console.log(result)  
    } catch (e) {  
        console.log(e)  
    }  
})


```




### 템플릿 엔진

동적인 결과를 정적인 파일에 담는 기능을 제공

대표적으로 ejs 사용


*ejs 사용설정*
`app.set('view engine', 'ejs');`


> EJS 는 기본적으로 views 폴더를 경로로 잡는다

`res.render('list.ejs', {data: result})`
view 폴더의 list.ejs 로 보냄, data라는 이름의 변수에 result 데이터 전송


<% %> 를 사용하여 js 코드를 안에 작성한다.

```
// Mongo Insert Form
<% for (let i = 0; i<data.length; i++){ %>  
<tr>  
    <td><%= data[i].title %></td>  
    <td><%= data[i].content %></td>  
    <td><button class = 'delete btn btn-outline-danger' >삭제</button></td>  
</tr>  
<% } %>

// MySQL Insert Form
<% for (let i = 0; i<data.length; i++){ %>  
<tr>  
    <td><%= data[i].title %></td>  
    <td><%= data[i].content %></td>  
    <td><%= data[i].created %></td>  
    <td><%= data[i].writer %></td>  
    <td><button class = 'delete btn btn-outline-danger' >삭제</button></td>  
</tr>  
<% } %>
```



---


### Source Code Link

<https://github.com/jyscode/boot_web/tree/main/node/D_0619>

1. npm i
2. .env 파일에 MONGO_URL 등록








