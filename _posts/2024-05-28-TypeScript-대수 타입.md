---
title: "대수 타입(Algebraic type)"
excerpt: ""

categories:
  - TypeScript
tags:
  - [TypeScript, 대수 타입]

permalink: /TypeScript/Algebraic_type/

toc: true
toc_sticky: true

date: 2024-5-28
last_modified_at: 2024-05-28
---

# 대수 타입

- 여러 개의 타입을 합성해서 만드는 타입

## 합집합(Union) 타입

- 바 `|`를 이용해서 정의
- 유니온 타입에 참여하는 타입의 개수에는 제한이 없다.

```ts
// 변수 타입 정의
let a: string | number; // string 타입이거나, number 타입

a = 1;
a = "hello";

let b: string | number | boolean;

b = 1;
b = false;
b = "hi";

// 배열 타입 정의
let arr: (number | string | boolean)[] = [1, "hello", true];

// 객체 타입 정의
type Dog = {
  name: string;
  color: string;
};

type Person = {
  name: string;
  language: string;
};

type Union1 = Dog | Person;

let union: Union1 = {
  name: "하진",
  language: "한국어",
};

let union2: Union1 = {
  name: "방방",
  color: "검은색",
  language: "멍멍",
};
```

## 교집합(Intersection) 타입

- `&`를 이용해서 정의
- 대다수의 기본 타입들 간에는 서로 공유하는 교집합이 없기 때문에 never 타입으로 추론된다.
  - 보통 객체 타입에서 자주 사용된다.

```ts
// 변수 타입 정의
let variable: number & string; // 교집합이 없음 => never 타입

// 객체 타입 정의
type Dog = {
  name: string;
  color: string;
};

type Person = {
  name: string;
  language: string;
};

type Intersection = Dog & Person;

let intersection: Intersection = {
  name: "",
  color: "",
  language: "",
};
```

<br/>

**참고자료**

- https://ts.winterlood.com/44460889-64bd-4d4d-83af-9983f598fd2d
