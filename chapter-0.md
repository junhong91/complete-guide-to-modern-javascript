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

