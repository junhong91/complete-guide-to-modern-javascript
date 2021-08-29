## arrow function
---
ES6에서 처음 도입됨  

```
var greeting = (name) => {
    return `hello ${name}`;
};
```

__매개변수가 1개만 존재한다면 괄호 생략 가능__

```
var greeting = name => {
    return `hello ${name}`;
};
```

#### 암시적 반환
다음과 같이 중괄호/return을 생략하고 사용 가능

```
const greeting = name => `hello ${name}`;
```

⚠️ 코드의 간결함 보다는, 가독성이 더 중요함. 암시적반환을 팀에서 숙지하지 못했다면, 사용하지 말자

<br>

#### arrow function and `this`
arrow function 내부에 `this` 키워드는 다르게 동작함!  
arrow function 내부에 `this` 키워드는 __상위 scope에서 상속됨__  

```
//HTML
<div class="bix open">
  this is a box
</div>

//CSS
.opening {
  background-color: red;
}

//JS
const box = document.querySelector(".box);
box.addEventListener("click", function() {
  this.classsList.toggle("opening");

  setTimeout(function() {
    this.classList.toggle("opening");
  } ,500);
});

```

해당 코드의 문제점은 __첫 번쨰 this는 const box에 할당되었지만, setTimeout 내부의 두 번째 this는 Window 객체로 설정됨__

> Uncaught TypeError: cannot read property "toggle" of undefined

이를 해결하기 위해서는, arrow function은 부모의 `this`를 상속한다는 것을 이용하면 됨  

```
const box = document.querySelector(".box");
box.addEventListener("click", function() {
  this.classList.toggle("opening");

  setTimeout(() => {
    this.classList.toggle("opening);
  } ,500);
})
```

<br>

#### arrow function 사용을 피해야하는 경우
arrow function에서 `this`는 상속된다는 점을 이해했다면 다음 상황이 문제가 될 수 있음을 인지 가능  

```
const button = document.querySelector("btn");
button.addEventListener("click", () => {
  // Error: 여기서의 this는 Window 객체
  this.classList.toggle("on");
});
```

```
const person1 = {
  age: 10,
  grow: function() {
    this.age++;
    console.log(this.age);
  }
}

person1.grow();
//11 not error
```

```
const person2 = {
  age: 10,
  grow: () => {
    // Error! 여기서 this는 Window 객체
    this.age++;
    console.log(this.age);
  }
}

person2.grow();
```

