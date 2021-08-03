## 0.2 자료형

---

> 자바스크립트는 동적언어(dynamic language)이다. 즉, 변수를 정의할 때, _자료형을 정의할 필요가 없다_

```
var userID;
userID = 12;
console.log(typeof userID); //number

userID = 'user1';
console.log(typeof userID); //string
```

자바스크립트를 엄격한 자료형을 준수하도록 강요하는 type script라는 언어 존재

<br>
<br>

## 원시(primitive) 자료형

---

modern javascript에서는 6가지 primitive 자료형 존재

- string: 문자열
- number: 숫자
- boolean: 불리언
- null: 널
- undefined: 정의되지 않음
- symbol: 심벌. ES6에서 추가됨

#### null vs undefined

null은 **값이 없음** 을 의미하고, undefined는 **정의되지 않은 값** 을 의미함

symbol은 _고유하고 변경할 수 없는 값_ 을 의미함

#### object

object는 여러 속성(property)의 모음을 저장할 수 있음

```
const car = {
    wheels: 4,
    color: "red",
}
```

object는 `key:value`로 구성된 집합  
key는 `string` 자료형만 가능  
value값은 모든 자료형 가능(함수도 가능)  

```
const car = {
    wheels: 4,
    color: "red",
    drive: function() {
        console.log("wroom wroom")
    },
};

console.log(Object.keys(car)[0]); //wheels
console.log(typeof Object.keys(car)[0]);    // string
car.drive();
```

<br>

#### empty object 생성
빈 객체를 생성하는 방법 2가지
```
1) const car = new Object();
2) const car = {};
```

두 번째 방법이 더 일반적으로 사용됨.  
이를 _object literal_ 이라고 함

빈 객체를 생성하고, 다음과 같이 새 속성 추가 가능
```
car.color = 'red';
console.log(car);   // {color: "red"}
```

_dot notation_ 을 사용하여 객체 car에 새 속성 추가

<br>

#### 객체 속성 접근 방법 2가지
1) _dot notation_
2) _bracket notation_

```
const car = {
    wheels: 4,
    color: "red"
};

console.log(car.wheels);    // 4
console.log(car['color']);   // red
```

왜 접근 방법이 2가지가 존재하는가?  
두 방법이 완전히 동일하지 않음  
__space가 있는 속성은 dot notation 사용 불가__

```
const car = {
    wheels: 4,
    color: "red",
    "goes fast": true
};

console.log(car.goes fast); //syntax error
console.log(car['goes fast']);  //true
```

아래와 같이 사용자의 입력을 받아서(scanf),  
입력 받은 값을 key로 value를 출력 가능  

```
const cars = {
    ferrari: "california",
    porshe: "911",
};

// user input
const key = "ferrari";
console.log(cars.key);  // undefined
console.log(cars['key']);   //undefined
console.log(cars["key"]);   // california
```
<br>

#### 객체의 복사
__primitive 자료형__ 과 달리, object를 복사할 때는 _참조(reference)_ 방식이 사용됨  

```
let car = {
    color: 'red',
};

let refCar = car;
```

여기서 `refCar`는 그 자체로 객체가 아닌, __car에 대한 참조__. 즉, __주소값(address)__ 를 저장함  

```
let car = {
    color: 'red',
};
let refCar = car;   //reference!

car.wheels = 4;
console.log(car);   // {color: 'red', wheels: 4}
console.log(refCar);    // {color:'red', wheels: 4}
```

항등 연산자(==) 를 이용하든, 완전 항등 연산자(===) 를 이용하든, true가 반환됨  
즉, 두 객체는 완전하게 동일함

```
console.log(car == refCar); //true
console.log(car === refCar);    //true
```

아래와 같이, 동일한 속성을 가진 객체끼리 비교는 항상 false를 리턴한다

```
const obj1 = {a: 1};
const obj2 = {a: 1};

obj1 == obj2;   // false
obj1 === obj2;  // false
```

object의 값 복사를 하려면, `assign()` 을 사용해야 함

```
const car = {
    color: 'red',
};
const secondCar = Object.assign({}, car);
car.wheels = 4;

console.log(car);   // {color:'red', wheels: 4}
console.log(secondCar); // {color:'red'}
```

<br>
<br>

## array

#### 배열 선언
> const fruits = ['banana', 'apple', 'orange'];

#### useful method

- `length` : 배열의 길이 리턴  
- `push()` : 배열의 끝에 값 추가  
- `unshift()` : 배열의 시작에 값 추가  
- `pop()` : 배열의 끝 값 제거  
- `shift()` : 배열의 시작 값 하나 제거

<br>
<br>

## scope
- global scope: 코드의 어느 곳에서나 접근 가능
- block scope: 블록 내부에서만 접근 가능

> 여기서 block이란 _function, loop, {}_ 로 구분되는 모든 영역을 의미함

`var` scope
```
var myInt = 1;

if (myInt === 1) {
    var mySecondInt = 2;
    console.log(mySecondInt);   //2
}

console.log(mySecondInt);   //2
```
⚠️ `var` 키워드로 선언된 변수 mySecondInt는 _block scope를 가지지 않는다_ 

`let` scope
```
var myInt = 1;

if (myInt === 1) {
    let mySecondInt = 2;
    console.log(mySecondInt);   //2
}
console.log(mySecondInt);   // Uncauht ReferenceError: mySecondInt is not defined
```

mySecondInt는 `let` 키워드로 선언 되었기 때문에, block scope를 가지므로 에러 발생

<br>

## `this` keyword

```
const myCar = {
    color: 'red',
    logColor: function() {
        console.log(this.color);
    },
};
myCar.logColor();   // red
```
여기서 `this` 키워드는 myCar object를 참조한다  

> `this` 값은 _호출되는 방식에 따라 달라진다._

```
function logThis() {
    console.log(this);
}
logThis();  // Window {...}
```
함수가 __전역 범위에서 호출__ 되었으므로, this값은 Window 객체를 참조함


