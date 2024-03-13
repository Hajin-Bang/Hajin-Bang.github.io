---
title: "this"
excerpt: "JavaScript의 this"

categories:
  - JavaScript
tags:
  - [this, JavaScript]

permalink: /JavaScript/this/

toc: true
toc_sticky: true

date: 2024-03-13
last_modified_at: 2024-03-13
---

# this

- this는 자신이 속한 객체 또는 자신이 생성할 인스턴스를 가리키는 자기 참조 변수이다.
- this 값은 **어떻게 함수가 호출되었는지**에 따라 달라진다.
- this가 참조하는 것을 **this 바인딩(binding)**이라고 한다.

## 전역 컨텍스트

- 전역 실행 컨텍스트에서 this는 전역 객체를 가리킨다.
- 브라우저에서는 window가 전역 객체이다.
  - Node.js에서는 global 객체가 전역 객체

```js
this; // 브라우저에서의 this: window
```

## 함수 컨텍스트

- 함수 내에서 this는 **함수가 어떻게 호출되었는지**에 따라 달라진다.

### 일반 함수 호출

- 전역에 선언된 함수에서의 this
- this는 전역 객체를 가리킨다.

```js
function show() {
  console.log(this);
}
show(); // window 객체 출력
```

> ❗️**엄격 모드(strict mode)에서는 일반 함수 호출 시 this가 `undefined`로 설정된다.**
>
> **엄격 모드(strict mode)** <br/>
> strict 모드는 ES5에 추가된 키워드로, 자바스크립트가 묵인했던 에러 메시지를 발생시킨다. <br/>
> 스크립트 시작 혹은 함수의 시작 부분에 `"use strict"`를 선언하면 strict 모드로 코드를 작성할 수 있다. <br/>
> 이는 모든 문법과 런타임 동작을 모두 검사하여, 실수를 에러로 변환하고, 변수 사용을 단순화 시켜준다.

### 메서드로서 호출

- 객체의 메서드로 함수를 호출할 때의 this
- this는 그 메서드를 호출한 객체를 가리킨다.

```js
const obj = {
  show: function () {
    console.log(this);
  },
};
obj.show(); //obj 출력
```

```js
const obj2 = {
  title: "hello world",
  show() {
    console.log(this.title); // this는 obj2를 가리킨다.
  },
};

obj2.show(); // 'hello world'
```

### 생성자 함수와 클래스

- `new`키워드와 함께 생성자 함수나 클래스를 호출할 때, this는 새로 생성된 인스턴스를 가리킨다.

```js
function Show() {
  this.title = "hello world"; // this는 새로 생성되는 객체를 가리킨다.
  return this;
}

const show = new Show();

console.log(show.title); // "hello world"
```

show 변수는 Show 생성자 함수에 의해 생성된 객체를 참조하게 되며, 이 객체는 `{ title: "hello world" }`형태의 속성을 갖게 된다.

### 화살표 함수

- 화살표 함수에서 this는 상위 스코프의 this값을 가진다.
- 화살표 함수는 함수를 선언할 때 this에 바인딩할 객체가 정적으로 결정된다.
- 선언된 위치에서 this값을 상속받는다.

```js
const obj = {
  show: () => {
    console.log(this);
  },
};

obj.show(); // 전역 객체
```

## 명시적 바인딩

- `call()`, `apply()`, `bind()` 메서드를 사용해서 this를 명시적으로 지정할 수도 있다.

**`call()`**

- `call`메서드는 첫번째 인자로 this에 바인딩할 객체를 받고, 그 뒤에는 실행할 함수의 인자들을 전달한다.
- `call`을 사용하면 함수가 즉시 실행된다.

```js
function greet(language, greeting) {
  console.log(`${greeting}! I speak ${language}. My name is ${this.name}.`);
}

const user = { name: "John" };
greet.call(user, "English", "Hello");
```

**`apply()`**

- `apply`메서드는 call과 유사하지만, 함수에 전달할 인자들을 배열 형태로 받는다.
- 함수가 즉시 실행된다.

```js
function greet(language, greeting) {
  console.log(`${greeting}! I speak ${language}. My name is ${this.name}.`);
}

const user = { name: "John" };
greet.apply(user, ["English", "Hello"]); // 인자가 배열 형태
```

**`bind()`**

- 함수를 즉시 실행하지 않는다.
- this값이 바인딩된 새로운 함수를 반환한다. 반환된 함수는 나중에 실행할 수 있다.
- 첫번째 인자로 this값으로 사요요할 객체를 받고, 그 뒤에는 바인딩할 함수를 전달한다.

```js
function greet(language, greeting) {
  console.log(`${greeting}! I speak ${language}. My name is ${this.name}.`);
}

const user = { name: "John" };
const greetUser = greet.bind(user, "English", "Hello");
greetUser(); // 나중에 호출
```

<br/>

**참고자료**

- https://hanamon.kr/javascript-this%EB%9E%80-%EB%AC%B4%EC%97%87%EC%9D%BC%EA%B9%8C/
- https://seungtaek-overflow.tistory.com/21
