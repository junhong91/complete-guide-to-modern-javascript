## Closure๋? ๐๏ธ

#### ํ์ค ์ ์

> a closure is a **function** that references variables in the outer scope from
> its inner scope.

- ํด๋ก์ ธ๋ ํจ์์๋๋ค
- ํด๋ก์ ธ๋ outer scope ์ ๋ณด๋ฅผ ์ฐธ์กฐํ๋ ํจ์์๋๋ค
  > The closure _preserves_ the outer scope inside its inner scope

ํด๋ก์ ธ ํจ์์ ์ ์์์ scope๋ผ๋ ๋จ์ด๊ฐ ๋ฑ์ฅํ๋๋ฐ,  
JS engine์ Lexical scoping์ ์ฌ์ฉํ๋ค

#### Scope๋? ๐ค

์ ์ธ๋ ๋ณ์์ ์ ๊ทผ ๊ฐ๋ฅํ ์ ํจ ๋ฒ์

#### Lexical Scope๋?

> _Lexical scope_(๋๋ _static scope_ ๋ผ๊ณ ๋ ํจ) defines how
> variable names are resolved in nested functions: **inner functions contain
> the scope of parent functions even if the parent function has returned**

๋ ๋ค๋ฅธ ์ข์ ์ ์๋ก๋

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

- ๋ชจ๋  inner level(`fun2`)์ outer level(`x`)์ ์ ๊ทผ ๊ฐ๋ฅ

[what is lexical scope?](https://stackoverflow.com/questions/1047454/what-is-lexical-scope)

#### Lexical scoping ์์ 

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

- `greeting()` ํจ์๋ local ๋ณ์ `message`์ `sayHi()` ํจ์๋ฅผ ์ ์
- `sayHi()` ํจ์๋ inner function์ผ๋ก, `greeting()` ํจ์๋ฅผ ํตํด์๋ง ํธ์ถ ๊ฐ๋ฅ
- `sayHi()` ํจ์๋ outer function์ ๋ณ์์ ์ ๊ทผ ๊ฐ๋ฅ

<br>

## Reference

- [JS clsoure](https://www.javascripttutorial.net/javascript-closure/)
- [ํ์ฟ ๋๋งํํ ํด๋ก์ ](https://hanamon.kr/javascript-%ED%81%B4%EB%A1%9C%EC%A0%80/)
