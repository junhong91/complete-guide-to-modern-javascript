## Closure란? 🛎️

#### 한줄 정의

> a closure is a **function** that references variables in the outer scope from
> its inner scope.

- 클로져는 함수입니다
- 클로져는 outer scope 정보를 참조하는 함수입니다
  > The closure _preserves_ the outer scope inside its inner scope

클로져 함수에 정의에서 scope라는 단어가 등장하는데,  
JS engine은 Lexical scoping을 사용한다

#### Scope란? 🤔

선언된 변수에 접근 가능한 유효 범위

#### Lexical Scope란?

> _Lexical scope_(또는 _static scope_ 라고도 함) defines how
> variable names are resolved in nested functions: **inner functions contain
> the scope of parent functions even if the parent function has returned**

또 다른 좋은 정의로는

> _Lexical scoping_ refers to **determining a variable's scope
> based on its position within the textual corpus of code**

```
void fun() {
  int x = 5;

  void fun2() {
    printf("%d", x);
  }
}
```

- 모든 inner level(`fun2`)은 outer level(`x`)에 접근 가능

[what is lexical scope?](https://stackoverflow.com/questions/1047454/what-is-lexical-scope)

#### Lexical scoping 예제

```
function greeting() {
  let message = "Hi";

  function sayHi() {
    console.log(message);
  }

  sayHi();
}

greeting();
```

- `greeting()` 함수는 local 변수 `message`와 `sayHi()` 함수를 정의
- `sayHi()` 함수는 inner function으로, `greeting()` 함수를 통해서만 호출 가능
- `sayHi()` 함수는 outer function의 변수에 접근 가능

<br>

## Reference

- [JS clsoure](https://www.javascripttutorial.net/javascript-closure/)
- [하쿠나마타타 클로저](https://hanamon.kr/javascript-%ED%81%B4%EB%A1%9C%EC%A0%80/)
