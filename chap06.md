## 06 디스트럭팅(destructing)

> Destructing이란 배열의 값 또는 객체의 속성을 풀어서 _별개의 변수로 쓸 수 있게 해주는 JS 표현식_

#### Object destructing

before ES6

```
var person = {
  first: "Alberto",
  last: "Monalesi",
}

var first = person.first;
var last = person.last;
```

After ES6 with destructing

```
var person = {
  first: "Alberto",
  last: "Monalesi",
}

const {first, last} = person;
```

디스트럭팅을 이용하여, **person이 가진 속성(first,last)에 접근함과 동시에 해당 속성 이름으로 변수 선언이 가능 함**

**중첩된 객체의 형태에서도 동일한 방법 적용 가능**

```
const person = {
  name: "Albetro"
  links; {
    social: {
      facebook: "https://somelink.com"
    }
  }
}

const { facebook } = person.links.social;
```

변수의 이름을 객체의 속성과 동일하게 지정하는데 그치지 않고,  
다음과 같이 변수의 이름을 바꿀 수 있다 -> `{nameBefore: nameNew}`

```
const { facebook: fb} = person.links.social;
console.log(fb);    // https://somelink.com 출력
consolg.log(facebook);  // ReferenceError: facebook is not defined
```

아래와 같이 default값 전달도 가능

```
const { facebook: fb = "https://somelink.com" } = person.links.social;
```

#### Array destructing

array destructing은 object destructing에서 사용했던 `{}` 대신 `[]`를 사용

```
const person = ["Alberto", "Montalesi", 25];
const [name, surname, age] = person;
```

생성하려는 변수의 수가 배열의 수보다 적다면?

```
const person = ["Alberto", "Montalesi", 25];
// age(25)는 필요하지 않으므로 뺀다
const [name, surname] = person;
// 25는 어떤 변수에도 할당되지 않음

console.log(name, surname);
// Alberto Montalesi
```

나머지 모든 값을 얻고 싶다면 rest operator(`...`)를 사용한다

```
const person = ["Alberto", "Montalesi", "pizza", "ice cream", "cheese cake"];
// Rest Operator를 사용하여 나머지 값 전체를 얻는다.
const [name, surname, ...food] = person;
console.log(food);
// ["pizza", "ice cream", "cheese cake"]
```

배열의 처음 두 값은 `name`과 `surname`에 할당됨  
나머지(Rest)는 food 배열에 할당. 그래서 Rest Operator

#### Swap variable using destructing

destructing을 사용하면, 변수를 매우 쉽게 swap 가능

```
let hungry = "yes";
let full = "no";

[hungry, full] = [ full, hungry];
```
