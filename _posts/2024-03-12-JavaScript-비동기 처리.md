---
title: "비동기 처리"
excerpt: "callback, Promise, asnyc/await에 대하여"

categories:
  - JavaScript
tags:
  - [callback, Promise, asnyc/await, 비동기, JavaScript]

permalink: /JavaScript/비동기-처리/

toc: true
toc_sticky: true

date: 2024-03-12
last_modified_at: 2024-03-12
---

# 비동기 처리

JavaScript의 비동기 처리란 특정 코드의 연산이 끝날 때까지 기다리지 않고 다음 코드를 실행하는 특성을 말한다. 동시에 여러가지 작업을 처리할 수 있고, 기다리는 과정에서 다른 함수를 호출할 수도 있다.

## callback

- 콜백 함수는 다른 함수가 실행을 끝난 뒤 실행하는 함수이다.
- 파라미터로 함수를 전달 받아서 함수 내부에서 실행한다.

```js
function add(a, callback) {
  setTimeout(() => callback(a + 5, 100));
  // 100ms가 지난 후 함수로 입력받은 callback에 a+5값을 다시 입력하여 callback함수 호출
}
add(10, function (res) {
  console.log(res);
});
```

> `setTimeout()`은 JavaScript에서 제공하는 내장 함수 중 하나로, **지정된 시간만큼 기다렸다가 로직을 실행하는 함수**이다. 이 함수는 비동기적으로 작동한다.
> 두개의 주요 인자를 받는다.
>
> - callback: 지정된 지연 시간 후에 실행될 함수
> - delay: 함수 실행 전 대기할 시간
>
> ```js
> setTimeout(function () {
>   console.log("3초가 지났습니다.");
> }, 3000);
> ```
>
> 이 코드는 3초(3000ms)가 지난 후에 "3초가 지났습니다"를 콘솔에 출력한다.

> callback을 n번 연속적으로 호출하게 되면, **콜백 지옥**이 발생한다. 이로 인해 유지보수성과 가독성이 떨어질 수 있다.

## Promise

- 프로미스란 생성된 시점에서 결과를 아직 반환하지 않은 객체를 뜻한다.
- 프로미스를 통해 **콜백지옥을 개선**할 수 있다.
- `then()`, `catch()`, `finally()` 메서드를 통해 성공, 실패, 완료 처리를 간결하게 할 수 있다.
  - `then()`: Promise가 성공적으로 완료되었을 때 실행될 콜백함수를 등록한다. 첫번째 인자는 'resolve'의 결과를 처리하고, 두번째 인자는 'reject'의 결과를 처리한다.
  - `catch()`: Promise가 실패했을 때 실행될 콜백 함수를 등록한다. 이는 'reject'의 결과를 처리한다.
  - `finally()`: Promise의 성공 여부와 상관없이 실행될 콜백 함수를 등록한다. 주로 리소스를 정리하거나, 최종적으로 어떤 작업을 수행할 때 사용한다.

### Promise의 세가지 상태

- pending(대기): 이행도, 거절도 안된 초기 상태
- fulfilled(이행): 비동기 연산이 성공적으로 완료된 상태, 결과값을 반환한다.
- rejected(실패): 비동기 연산에 실패한 상태, 에러를 반환한다.

```js
function add(a) {
  return new Promise((resolve, reject) => {
    setTimeosut(() => resolve(a + 5), 100);
  });
}

add(10).then((res) => {
  console.log(res);
});
```

위는 callback 기반의 add 함수를 Promise 사용 방식으로 변경한 코드이다. <br/>
Promise의 실행자 함수 내에서 setTimeout을 사용하여 결과를 Resolve한다. Promise가 성공적으로 완료되면, `then()`에 등록된 콜백 함수가 호출되어 결과를 출력한다. <br/>
이렇게 하면, 각 콜백 함수마다 에러 처리 로직을 구현해야하는 콜백 방식과 달리, Promise 한 곳에서 모든 에러를 캐치할 수 있다는 장점이 있다.

```Js
const createPromise = () => new Promise((resolve, reject) => {
  // Promise 객체를 생성하고 반환한다
  let a = 1 + 1

  if (a == 2) {
    resolve('success')
  } else {
    reject('failed')
  }
})

createPromise().then((message) => { // then 메서드를 통해 resolve의 결과인 'success'문자열을 받는다
  console.log('This is in th then ' + message)
}).catch((message) => { // catch 메서드를 통해 에러 메시지를 받는다
  console.log('This is in the catch' + message)
})
```

### Promise chaining

- 프로미스 체이닝은 여러 개의 Promise를 연결하여 순차적으로 비동기 작업을 실행하는 방법을 말한다.
- 비동기 작업을 마치 동기 작업처럼 순서대로 처리할 수 있으며, 코드의 가독성도 향상된다.

## async/await

- **Promise를 더 쉽고 직관적으로 사용할 수 있도록** ES8에 추가된 문법이다.
- 비동기 코드를 동기 코드처럼 보이게 하여 더 읽기 쉽게 만든다.
- `async`가 붙은 함수는 항상 프로미스를 반환한다.
- 비동기로 처리되는 부분에 `await`를 붙이면 해당 프로미스가 끝날 때까지 기다린다. (동기적으로 처리)
  - await 키워드를 사용하면 일반 비동기 처리처럼 바로 실행이 다음 라인으로 넘어가는 것이 아니라, 결과 값을 얻을 수 있을 때 까지(await) 기다려주기 때문에 일반적인 동기 코드처리와 동일한 흐름으로 코드를 작성할 수 있다.
- try/catch를 사용하여 에러를 처리할 수 있다.

```js
async function add(a) {
  const result = await new Promise((resolve, reject) => {
    setTimeout(() => resolve(a+5), 100);
  });
  return result;
}

async functino result() => {
  const res = await add(10);
  console.log(res);
}

result();
```

```js
async function createPromise() {
  return new Promise((resolve, reject) => {
    let a = 1 + 1;

    if (a == 2) {
      resolve("success");
    } else {
      reject("failed");
    }
  });
}

// 함수 사용
async function result() => {
  try {
    const message = await createPromise();
    console.log("This is in the then " + message);
  } catch (message) {
    console.log("This is in the catch " + message);
  }
}

result();
```

<br/>

**참고자료**

- https://velog.io/@syoung125/JS-Promise%EB%9E%80
- https://gonggongnote.tistory.com/54
- https://yoo11052.tistory.com/165
