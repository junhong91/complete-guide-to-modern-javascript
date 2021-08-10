## 1.1 `var`, `let`, `const` 차이점

---

#### `var`
var 키워드로 선언된 변수는 _function scope를 가진다_  
단, **for loop 내부에서 사용된 `var` 변수는 for loop 밖에서도 사용 가능**

```
for (var i = 0; i < 10; i++) {
    var leak = "I am available outside of the loop";
}

console.log(leak);  // I am available outside of the loop

function myFunc() {
    var functionScoped = "I am available insde this function";
    console.log(functionScoped);
}
myFunc();

console.log(functionScoped);    // ReferenceError: functionScoped is not defined
```

#### `let`
`let` / `const` 키워드로 선언된 변수는 _block scope를 가진다_  

###### what is block scope?
변수가 선언된 블록에서 사용 가능  
변수가 선언된 블록 하위에서 사용 가능

```
let x = "global";
if (x === "global") {
    let x = "block-scoped";

    console.log(x); //block-scoped
}
console.log(x); //global

var y = "global";
if (y === "global") {
    var y = "block-scoped";
    console.log(y); //block-scoped;
}
console.log(y); //block-scoped
```

#### `const`
`let`과 동일하게 _block scope를 가짐_  
단 차이점은, `let`과 다르게 __값의 재할당이 불가능함__  

> ⚠️ const로 선언된 변수가 __불변은 아님__  

#### `const`에 객체가 담겼다면?
```
const person = {
    name: "alberto",
    age: 25,
};

person.age = 26;    //possible
console.log(person.age);    // 26
```

이 경우, 변수 전체(person)를 재할당하는 것이 아닌  
그 속성값을 재할당하는 것이므로 문제가 없음!

#### ⚠️ NOTE  
const object 자체의 값을 변경하려고 시도할 때, Javascript는 오류를 던지지 않는다  

```
const person = {
    name: "alberto",
    age = 25,
};

person.age = 26;
console.log(age);   //26

Object.freeze(person);

person.age = 30;
console.log(person.age);    // 26
```

<br>

## TDZ(Temporal Dead Zone)
---

```
console.log(i);
var i = "I am a variable";

// undefined

console.log(j);
let j = "I am a let";

// ReferenceError: can't access lexical declaration 'j' before initialization
```

- `var`는 __정의되기 전에 접근 가능하다__
- `var`는 정의되기 전에 접근 가능하나, __그 값에는 접근 할 수 없다(undefined)__

<br>

- `let`, `const`는 __정의되기 전에 접근 불가능__


#### ⚠️ NOTE
`var`, `let`, `const` 모두 다른 source file에서 읽을 수 있는 내용임에도 불구하고  
hoisting의 대상이 됨  
즉, 코드가 실행되기 전에 처리되고, 해당 스코프 상단으로 올라감  

##### Conclusion
`var`가 가지는 가장 큰 차이점은 정의 되기 전에 접근이 가능하다는 점  
반면, `let`, `const`는 정의될때까지 TDZ 영역에 존재하게 됨  

__따라서 `const`나 `let`이 더 디버깅 하기 쉬움__  

<br>

## 언제 `var`, `let`, `const`를 사용해야 하는가?
---

- 기본적으로 `const`를 쓴다
- 재할당이 필요할 때만 `let`을 쓴다
- `var`는 ES6에서 절대 사용하지 않는다



