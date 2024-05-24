---
title: "기본 타입 호환성"
excerpt: "기본 타입에서의 타입 호환성, 업 캐스팅과 다운 캐스팅"

categories:
  - TypeScript
tags:
  - [TypeScript, 타입 호환성, 업 캐스팅, 다운 캐스팅]

permalink: /TypeScript/기본_타입_호환성/

toc: true
toc_sticky: true

date: 2024-5-24
last_modified_at: 2024-05-24
---

# 타입 호환성

- 하나의 타입을 다른 타입으로 취급해도 괜찮은지 판단하는 것
- 예를 들어, A와 B의 두 개의 타입이 존재할 때, A 타입의 값을 B 타입으로 취급해도 괜찮은지 판단하는 것을 의미한다.
- A 타입의 값이 B 타입의 값으로 취급 되어도 괜찮다면 호환된다고 말한다.

**예시1** <br/>
Number 타입과 Number 리터럴 타입

- Number 리터럴 타입을 Number 타입의 값으로 취급하는 것이 가능하다.
- 반대로, Number 타입을 Number 리터럴 타입의 값으로 취급하는 것은 불가능하다.

어떻게 판단하는 것일까?

- Number타입이 Number 리터럴 타입보다 더 큰 타입이기 때문이다.
  - Number 타입: 슈퍼타입, Number 리터럴 타입: 서브타입

코드로 살펴보자.

```ts
let num1: number = 10; // Number 타입
let num2: 10 = 10; // Number 리터럴 타입

num1 = num2; // num1에 num2의 값을 할당할 수 있다.
num2 = num1; // 불가능 => Number 리터럴 타입이므로 Number 타입의 값이 할당될 수 없다.
```

따라서 TypeScript는 서브타입의 값을 슈퍼타입의 값으로 취급하는 것은 가능하나, 슈퍼타입의 값을 서브타입의 값으로 취급하는 것은 허용하지 않는다.

## 업 캐스팅

- 서브 타입의 값을 슈퍼타입의 값으로 취급하는 것
- TypeScript는 업 캐스팅을 모든 상황에 허용한다.

## 다운 캐스팅

- 슈퍼타입의 값을 서브타입으로 취급하는 것
- TypeScript에서는 대부분의 다운 캐스팅이 불가능하다.

## 타입 계층도

타입 계층도를 통해 타입 간의 관계를 확인하면 타입 호환성에 대해 이해할 수 있다.

![image](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F593968f2-7c02-45ab-b152-66202eb4a8c2%2FUntitled.png?table=block&id=fcf12561-2c5d-46f0-9fca-db34ecddbcca&cache=v2)

### unknown 타입 (전체 집합)

- 타입 계층도의 최상단에 위치한다. => 모든 타입의 슈퍼타입
- 즉 unknown 타입의 변수에는 모든 타입의 값을 할당할 수 있다.
- 반대로, 다른 타입의 값에 unknown 타입을 할당하는 것은 대부분 불가능하다.
  - any 타입만 허용

```ts
let a: unknown = 1; // number 타입의 값 할당 가능
let b: unknown = "hello"; // string 타입의 값 할당 가능

let unknownValue: unknown;
let c: number = unknownValue; // 불가능
```

### never 타입 (공집합)

- 타입 계층도의 가장 아래에 위치한다. => 모든 타입의 서브타입
- 공집합을 뜻한다. => 아무것도 포함하지 않는 집합
- never 타입은 어떤 타입에도 할당될 수 있다. (모든 타입으로 업캐스팅 가능)
- 반대로, never 타입에는 어떤 타입의 값도 할당될 수 없다. (어떤 타입도 never 타입으로 다운캐스팅 불가능)

```ts
let neverVar: never;

let a: number = neverVar; // number 타입의 값에 never 타입 할당
let b: string = neverVar;
let c: boolean = neverVar;
let d: null = neverVar;
let e: undefined = neverVar;
let f: [] = neverVar;
let g: {} = neverVar;

let aa: never = 1; // 불가능 (never 타입에는 어떤 타입의 값도 할당될 수 없다.)
let bb: never = "hello"; // 불가능
```

### void 타입

- 아무것도 반환하지 않는 함수의 반환값으로 주로 사용되는 타입
- undefined, never의 슈퍼타입
- void로 선언한 함수에서 undefined, never를 반환하는 것이 가능하다.
  - 그 외의 타입의 값은 할당할 수 없다.

```ts
function noReturnFunctionA(): void {
  return undefined;
} // void 함수에서 undefined 타입 반환

let voidVar: void;

voidVar = undefined; // void 타입의 값에 undefined 할당
voidVar = "hello"; // 불가능
```

### any 타입 (치트키)

- 타입 계층도를 완전히 무시하는 치트키 타입
- 모든 타입의 슈퍼타입이 될 수 있고, 모든 타입의 서브타입이 될 수도 있다.
- 하지만 안전하지 못하므로 최대한 사용하지 않는 것이 좋다.

<br/>

**참고자료**

- https://ts.winterlood.com/9610eed7-2b66-4645-9181-483243a2089a
- https://ts.winterlood.com/1d6906f2-b724-43d0-bc61-8ec455e6d8e8
