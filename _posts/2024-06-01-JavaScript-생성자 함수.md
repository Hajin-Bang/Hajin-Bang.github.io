---
title: "생성자 함수"
excerpt: ""

categories:
  - JavaScript
tags:
  - [JavaScript, 생성자 함수]

permalink: /JavaScript/생성자_함수/

toc: true
toc_sticky: true

date: 2024-06-01
last_modified_at: 2024-06-01
---

# 생성자 함수

- new 연산자와 함께 호출하여 객체(인스턴스)를 생성하는 함수
  - 만약 new 연산자와 함께 호출하지 않으면, 생성자 함수가 아니라 일반 함수로 동작한다.

```js
const person = new Object();

person.name = "방하진";
person.sayHello = function () {
  console.log("hi");
};
```

> **객체**
>
> - 속성을 통해 여러 개의 값을 하나의 단위로 구성한 자료구조
> - 객체 지향 프로그래밍: 독립적인 객체의 집합으로 프로그램을 표현하려는 패러다임
>   - 상태, 동작 => 상태 데이터와 동작을 하나의 논리적인 단위로 묶은 복합적인 구조
>   - 프로퍼티(상태), 메서드(동작)

## 생성자 함수의 장점

- 마치 객체(인스턴스)를 생성하기 위한 템플릿(클래스)처럼 프로퍼티 구조가 동일한 객체 여러 개를 간편하게 생성할 수 있다.

```js
function Circle(radius) {
  this.radius = radius;
  this.getDiameter = function () {
    return 2 * this.radius;
  };
}

// 인스턴스 생성
const circle1 = new Circle(5);
const circle2 = new Circle(10);

console.log(circle.getDiameter()); // 10
```

> ### 객체 리터럴에 의한 객체 생성 방식의 문제점
>
> 객체 리터럴에 의한 객체 생성 방식은 직관적이고 간편하다. 하지만 이는 단 하나의 객체만 생성할 수 있다. 따라서 동일한 프로퍼티를 갖는 객체를 여러 개 생성해야 하는 경우 매번 같은 프로퍼티를 기술해야 하기 때문에 비효율적이다.

## new 연산자

- new 연산자와 함께 함수를 호출하면 해당 함수는 생성자 함수로 동작한다.

```js
function add(x, y) {
  return x + y;
}

let inst = new add();
// 생성자 함수로서 정의하지 않은 일반 함수를 new 연산자와 함께 호출

console.log(inst); // {} => 함수가 객체를 반환하지 않으므로 빈 객체가 생성되어 반환된다.

// 객체를 반환하는 일반 함수
function createUser(name, role) {
  return { name, role };
}

inst = new createUser("Lee", "admin");

console.log(inst); // {"Lee", "admin"}
// 함수가 생성한 객체를 반환한다.
```

## new.target

- 생성자 함수가 new 연산자 없이 호출되는 것을 방지하기 위해 지원하는 ES6의 메타 프로퍼티
- new.target은 함수 자신을 가리킨다.
  - new 연산자 없이 일반 함수로서 호출된 함수 내부의 new.target은 undefined이다.
- new 연산자와 함께 생성자 함수로서 호출되었는지 확인할 수 있다.

```js
function Circle(radius) {
  if (!new.target) {
    // new 연산자와 함께 호출했는지 확인
    return new Circle(radius);
    // new 연산자와 함께 생성자 함수를 재귀 호출하여 생성된 인스턴스를 반환
  }
  this.radius = radius;
  this.getDiameter = function () {
    return 2 * this.radius;
  };
}

const circle = Circle(5);
// new 연산자 없이 생성자 함수를 호출하였지만, 위의 조건문(new.target)에 의해 생성자 함수로서 호출된다.
```
