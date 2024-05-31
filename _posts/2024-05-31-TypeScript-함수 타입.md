---
title: "함수 타입"
excerpt: ""

categories:
  - TypeScript
tags:
  - [TypeScript, 함수 타입]

permalink: /TypeScript/함수_타입/

toc: true
toc_sticky: true

date: 2024-5-31
last_modified_at: 2024-05-31
---

# 함수 타입

## 함수 타입 정의

- 매개변수의 타입 정의
- 반환값 타입 정의
  - 반환값 타입은 매개 변수를 통해 자동으로 추론되기 때문에 생략 가능하다.

```ts
function func(a: number, b: number): number {
  return a + b;
}

// 화살표 함수 타입 정의
const add = (a: number, b: number): number => a + b;
// 기본 함수와 동일하게 반환값은 명시하지 않아도 자동으로 추론된다.
```

## 매개변수 관련 설정

### 기본값 설정

- 매개변수에 기본값이 설정되어있으면 타입이 자동으로 추론된다.
  - 타입 정의 생략 가능

```ts
function func(name = "방하진") {
  console.log(`name: ${name}`);
}
```

### 선택적 매개변수 설정

- `?`를 붙여서 선택적 매개변수를 정의할 수 있다.
- 필수 매개변수 앞에 위치할 수 없다.
  - 반드시 필수 매개변수를 모두 정의한 후, 뒤에 배치해야한다.
- undefined와 유니온 된 타입으로 추론된다.

```ts
function introduce(name = "방하진", age?: number) {
  // age의 타입은 number | undefined 가 된다.
  console.log(`name: ${name}`);
  console.log(`age: ${age}`);
}

introduce("방하진"); // age 매개변수는 사용하지 않아도 된다.
introduce("방하진", 25);

// 위에서 age의 타입은 number 이거나 undefined 타입으로 정의되었다.
// 이 때 age값이 있는, 즉 number 타입으로 추론되었다고 기대하고 사용하려면 아래와 같은 타입 좁히기가 필요하다.
function introduce(name = "방하진", age?: number) {
  console.log(`name: ${name}`);
  if (typeof age === "number") {
    console.log(`age: ${age}`);
  }
}
```

### 나머지 매개변수 (rest 파라미터)

- 개별 요소를 배열로 묶는 기능을 하는 파라미터
- 먼저 선언한 매개변수에 할당된 인수를 제외하고 나머지를 모두 배열에 저장한다.
  - 반드시 매개변수에서 마지막에 선언되어야한다.

```ts
function getSum(...rest: number[]) {
  // 배열의 타입을 명시하면 된다.
  let sum = 0;
  rest.forEach((it) => (sum += it));
  return sum;
}

getSum(1, 2, 3); // 매개변수: [1, 2, 3]

// 매개변수 길이를 고정하고 싶다면 튜플 타입을 이용하면 된다.
function getSum(...rest: [number, number, number]) {
  // 배열의 길이는 무조건 3
  let sum = 0;
  rest.forEach((it) => (sum += it));
  return sum;
}

getSum(1, 2, 3);
getSum(1, 2, 3, 4); // 불가능
```

## 함수 타입 표현식

- 타입 별칭과 함께 별도로 함수 타입을 정의하는 표현식
- 여러 개의 함수가 동일한 타입을 갖는 경우에 사용할 수 있다.

```ts
type Add = (a: number, b: number) => number;

const add: Add = (a, b) => a + b;
```

## 호출 시그니처

- 함수 타입 표현식과 동일하게 함수의 타입을 별도로 정의하는 방식
- 객체를 정의하듯 함수의 타입을 정의할 수 있다.

```ts
type Operation = {
  (a: number, b: number): number;
};

const add: Operation = (a, b) => a + b;
const multiply: Operation = (a, b) => a * b;
```

<br/>

**참고자료**

- https://ts.winterlood.com/0fe19fd9-39ca-4e40-9aea-fe1cc68403ba
