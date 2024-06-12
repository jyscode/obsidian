
`변수 지정 : var`
자바스크립트에서는 변수에 어떤 타입이든 들어갈 수 있다.

```js
// String to Number

var msg = 'hello'  
msg = 100  
console.log(msg)
```


### 변수 이름 짓기

- 변수의 첫 글자를 특수문자나 숫자로 시작할 수 없다
- 변수의 첫 글자는 영문자이거나 언더스코어만 된다.
- 자바스크립트는 대소문자를 구분한다.
- 변수의 이름이 여러 단어일 경우 \_를 사용하거나 대문자로 구분한다(Camel case).
- JS에서 사용하는 예약어를 변수명으로 사용할 수 없다. ex) var, if



### Javascript 데이터 타입

Number
- 숫자형 타입으로 계산 불가능한 경우 에러가 아닌 NaN 으로 반환
- 문자열 타입 앞에 +를 붙이면 Number Type으로 변환 `+"1024"`
String
- 문자열 타입으로 + 기호로 연결 가능, 다른 데이터 타입과 + 로 연결 시 type은 String
- 문자열의 길이 구하기 .length
Boolean
- 참과 거짓을 나타내는 타입 true, false 로 구성
Null
- 빈 값을 나타내는 타입, 사용자가 의도적으로 대입하는 값
Undefined
- 정의되지 않은 상태, 변수를 선언하고 값을 할당을 하지 않은 상태
Object
- Object 형은 Call By Reference 를 사용한다.


> [!NOTE]
> JS는 오류에 관대한편으로 자료형으로 인한 에러가 잘 발생하지 않는다.



---

### Javascript Object 생성법

1. 객체 리터럴 이용
`var p1 = {name: "김지용"}`

2. Object 생성자 이용
`var p2 = new Object() p2.name = "김지용"`

3. 사용자 지정 생성자 사용
```
function Person(name){
	this.name = name
}

var p3 = new Person("김지용")

// 익명함수 사용
var Person = function(name){
	this.name = name
}
var p4 = new Person("김지용")
```

---

### Object Method

```js
const person = {  
  firstName: "John",  
  lastName: "Doe",  
  id: 5566,  
  fullName: function() {  
    return this.firstName + " " + this.lastName;  
  }  
};
```

person 이라는 Object 안에 fullName Method 생성

```js
// fullName() method 불러오기, return 값 반환
// 이때 name은 string 객체를 저장하므로 Call by Value
name = person.fullName()
// 객체 안의 fullName() 호출 Call by Reference
console.log(person.fullName())


// 새로운 메서드 추가, string의 toUpperCase() 함수를 사용하여 대문자로 변환한 결과 값을 return
person.name = function () {  
    return (this.firstName + " " + this.lastName).toUpperCase()  
}

// 기존 메서드 변경
person.fullName = function () {  
    return (this.firstName + " " + this.lastName).toUpperCase()  
}

// call by value  - John Doe
console.log(name)  
  
// call by reference  - JOHN DOE
console.log(person.fullName())



```



### Object Display

javascript를 웹상에서 출력하는 방법
- script 태그 안에 js 코드를 넣고 특정 태그에 innerHTML을 하는 방식을 사용
```html
<!DOCTYPE html>
<html>
<body>
<h1>JavaScript Objects</h1>
<p>Displaying a JavaScript object will output [object Object]:</p>

<p id="demo"></p>

<script>
// Create an Object
const person = {
  name: "John",
  age: 30,
  city: "New York"
};

// Display Object
document.getElementById("demo").innerHTML = person;
</script>

</body>
</html>

```

```js
// [object Object]
const person = {  
    name: "John",  
    age: 30,  
    city: "New York"  
}  

// name John age 30 city New York
// person 안에 객체를 순회 하며 key값을 출력
// Build a Text  
let text = "";  
for (let x in person) {  
    text += x + " " + person[x] + " ";  
}  
  
// Create an Array
// John,30,New York
const myArray = Object.values(person);  
  
  
const fruits = {Bananas:300, Oranges:200, Apples:500};  

// Bananas: 300  
// Oranges: 200  
// Apples: 500
let text2 = "";  
// key, value  
for (let [fruit, value] of Object.entries(fruits)) {  
    text2 += fruit + ": " + value + "<br>";  
}  
  
// Object to String  
// {"name":"John","age":30,"city":"New York"}
let myString = JSON.stringify(person);  
  
// String to Object  
// [object Object]
let toObject = JSON.parse(myString)

```


### Object Constructor

```js
function Person(first, last, age, eye) {  
    this.firstName = first;  
    this.lastName = last;  
    this.age = age;  
    this.eyeColor = eye;  
}
```

인자로 first, last, age, eye 를 받는 생성자 정의

`const myFather = new Person("John", "Doe", 50, "blue");`

parameter에 값을 넣어 객체 생성
```
// 출력 결과
Person {
  firstName: 'John',
  lastName: 'Doe',
  age: 50,
  eyeColor: 'blue'
}

```
```js
function Person2(first, last, age, eyecolor) {  
    this.firstName = first;  
    this.lastName = last;  
    this.age = age;  
    this.eyeColor = eyecolor;  
    this.nationality = "English";  
}
```

Default Value로 nationality 속성 생성 및 초기화

```
const mySelf = new Person2("Johnny", "Rally", 22, "green");

// 출력 결과
Person2 {
  firstName: 'Johnny',
  lastName: 'Rally',
  age: 22,
  eyeColor: 'green',
  nationality: 'English'
}

```

메서드 추가하기

```js
// 해당 객체에 메서드 추가 (정상)
myMother.changeName = function (name) {  
    this.lastName = name;  
}

myMother.changeName("Doe");



// object에 메서드 추가  
Person.changeName = function (name) {  
    this.lastName = name;  
}

// 에러 changeName is not a function
mySister.changeName("Doe");


// prototype에 메서드 추가 (정상)
Person.prototype.changeName = function (name) {  
    this.lastName = name;  
}
mySister.changeName("Doe");



```


native object 생성하기

```
new Object()   // A new Object object  
new Array()    // A new Array object  
new Map()      // A new Map object  
new Set()      // A new Set object  
new Date()     // A new Date object  
new RegExp()   // A new RegExp object  
new Function() // A new Function object


"";           // primitive string  
0;            // primitive number  
false;        // primitive boolean  
  
{};           // object object  
[];           // array object  
/()/          // regexp object  
function(){}; // function
```

