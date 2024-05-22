---
title: "배열, 튜플, 객체"
excerpt: "TypeScript의 배열과 튜플, 그리고 객체"

categories:
  - TypeScript
tags:
  - [TypeScript, 배열, 튜플, 객체]

permalink: /TypeScript/배열과 객체/

toc: true
toc_sticky: true

date: 2024-5-23
last_modified_at: 2024-05-23
---

# 배열, 튜플, 객체

## 배열

### 타입 정의 방법

- 방법 1 > 변수 이름 뒤에 `: 배열요소타입[]`을 작성한다.
- 방법 2 > 변수 이름 뒤에 `Array<배열요소타입>`을 작성한다.

```ts
let numArr: number[] = [1, 2, 3];
let strArr: string[] = ["HI", "IM", "HAJIN"];
let boolArr: Array<boolean> = [true, false, true];
```

### 다양한 타입 요소를 가질 경우

- 바(`|`)를 이용해 여러 타입을 작성한다.

```ts
let multiArr: (number | string)[] = [1, "hajin"];
```

### 다차원 배열

- `배열요소타입[][]`처럼 []를 연달아 작성해 정의할 수 있다.

```ts
let doubleArr: number[][] = [
  [1, 2, 3],
  [4, 5],
];
```

## 튜플

- 길이와 타입이 고정된 배열
- JavaScript에는 없는 TypeScript의 특수한 타입이다.

```ts
let tup1: [number, number] = [1, 2]; // 길이가 2로 고정된 number 타입 요소를 갖는 튜플
let tup2: [number, string] = [1, "hello"]; // 다양한 타입을 갖는 튜플도 정의할 수 있다.
```

> ### 튜플을 사용하는 이유
>
> TypeScript에서 튜플을 컴파일하면, 결국 JavaScript 배열로 변환되는 것을 알 수 있다. <br/>
> 그렇다면 튜플은 왜 사용하는 것일까?
>
> ```ts
> const users: [string, number] = [
>   ["방하진", 1],
>   ["방방방", 2],
>   ["하하하", 3],
>   [4, "진진진"], // 오류 발생
> ];
> ```
>
> 위와 같은 상황에서, 배열의 요소 순서를 잘못 배치해 추가할 경우 JavaScript는 오류를 확인할 방법이 없다. 하지만 TypeScript에서 튜플을 사용하면 위와 같은 실수를 빠르게 바로잡을 수 있다.

## 객체

### 타입 정의 방법

#### object

- 단순 값이 객체임을 표현하는 것 외에는 아무런 정보도 제공하지 않는 타입이다.
- 객체의 프로퍼티에 대한 정보를 가지고 있지 않는다.
- 따라서 객체의 특정 프로퍼티에 접근하려고 하면 오류가 발생한다.
- 객체의 구조를 그대로 타입으로 만들고싶다면, object가 아닌 객체 리터럴 타입을 이용해야 한다.

#### 객체 리터럴 타입

- 객체가 갖는 프로퍼티를 직접 나열해 만드는 타입
- 타입 내에 정의되어있는 프로퍼티에 접근할 수 있다.

```ts
let user: {
  id: number;
  name: string;
} = {
  id: 1,
  name: "방하진",
};

user.id; // 프로퍼티에 접근 가능
```

### 특수한 정의 (?, readonly)

#### 선택적 프로퍼티 (Optional Property)

- 특정 프로퍼티를 상황에 따라 생략하도록 만들고싶을 때 사용한다.
- 프로퍼티 이름 뒤에 `?`를 붙여주면 선택적 프로퍼티를 설정할 수 있다.

```ts
let user: {
  id?: number;
  name: string;
} = {
  name: "방하진", // id 프로퍼티를 생략할 수 있다.
};
```

#### 읽기 전용 프로퍼티 (Readonly Property)

- 특정 프로퍼티를 읽기 전용으로 만들고싶을 때 사용한다.
- 프로퍼티 이름 앞에 `readonly`를 붙여준다.
- 값을 수정하려고 하면 오류가 발생한다.

```ts
let user: {
  id?: number;
  readonly name: string;
} = {
  id: 1,
  name: "방하진",
};

user.name = "방방방"; // 오류 발생 => readonly 프로퍼티이므로 값을 변경할 수 없다.
```

  <br/>

**참고자료**

- https://ts.winterlood.com/43888ee0-9227-4a8d-994e-2336ee78bfcf
- https://ts.winterlood.com/1c336fb6-1a90-4076-8de1-b23810a65163
