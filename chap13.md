## Chapter 13. Promise

---

JS 코드는 `동기적`으로 동작함  
각 코드 블록이 이전 블록이후 실행됨

```
const data = fetch('your-api-goes-here');
console.log('Finished');
console.log(data);
```

동기 코드의 경우, fetch 작업이 완료된 후, 다음 행이 호출될 거라 예상함  
하지만, 실제로는 console.log(data)의 값은 `undefined`를 출력함

이러한 현상이 발생하는 이유는, `fetch` 함수가 `비동기적`으로 수행되기 때문
즉, 해당 `fetch`가 완료될 때까지 코드 실행을 중지하는게 아니라, 계속해서 다음 행을 실행함

이 문제를 해결하기 위해, callback 혹은 promise를 사용하면, `fetch`가 무언가를 반환하는 시점까지 기다리게 해야 함

#### 13.1 콜백 지옥

비동기 코드를 동기식으로 작동하는 것 처럼 하기 위해 `callback`사용  
여러 코드 블록을 연결해 작성하는 과정에서 `callback hell`이 발생

```
const makePizza = (ingredients, callback) => {
  mixIngredients(ingredients, function(mixedIngredients)) {
    bakePizza(mixedIngredients, function(bakePizza)) {
      console.log('Finished!');
    }
  }
}
```

콜백 지옥 개선 방법은 [callbackhell](http://callbackhell.com)을 참고

#### 13.2 `promise`

`promise`의 정의

> promise는 비동기 작업의 최종 성공 또는 실패를 나타내는 객체이다

```
const myPromise = new Promise((resolve, reject) => {
 // Write a code!
});
```

promise의 성공을 알림 => `resolve`  
promise의 실패를 알림 => `reject`

promise 안에서 즉시 `resolve`를 호출하면 어떤 값이 반환될까?

```
const myPromise = new Promise((resolve, reject) => {
  resolve("The value we get from the promise");
})

myPromise.then(
  data => {
    console.log(data);
  }
)
```

`resolve` 함수의 첫 번째 매개변수로 전달된 값이 콘솔에 출력됨

```
const myPromise = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve("The value we get from the promise");
  }, 2000);
});

myPromise.then(
  data => {
    console.log(data);
  }
)
// 2초가 지난 후
// The value we get from the promise
```

다음은 `reject`를 이용한 오류 처리 방법을 배운다

```
const myPromise = new Promise((resolve, reject) => {
  setTimeout(() => {
    reject(new Error("this is our error"));
  }, 2000);
});

myPromise.then(data => {
  console.log(data);
}).catch(err => {
  console.error(err);
});

// Error: this is our error
// Stack trace:
// myPromise</@debugger eval code:3:14>
```
