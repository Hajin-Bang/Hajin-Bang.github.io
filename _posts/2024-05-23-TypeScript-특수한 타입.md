---
title: "TypeScript만의 특수 타입"
excerpt: "TypeScript의 특수한 타입 any, unknown, void, never"

categories:
  - TypeScript
tags:
  - [TypeScript, any, unknown, void, never]

permalink: /TypeScript/Type/

toc: true
toc_sticky: true

date: 2024-5-23
last_modified_at: 2024-05-23
---

# TypeScript만의 특수한 타입

## any

- 타입 검사를 받지 않는 특수한 치트키 타입
- 어떤 타입으로 정의된 변수든 문제 없이 모두 할당할 수 있다.
  - 범용적으로 사용되어야 하는 변수에 적용
- 최대한 사용하지 않는 것이 좋다.
  - 타입 검사가 제대로 이루어지지 않기 때문에 런타임 시 오류가 발생하는 경우가 많다.

```ts
let anyVar: any = 10;
anyVar = "hello"; // any 타입이기 때문에 다른 타입의 값을 할당할 수 있다.

anyVar = ture;
anyVar = {};
// 어떤 값으로든 재할당 가능

anyVar.toUpperCase();
```

```ts
let anyVar: any = 10;
let str: string = "hajin";
str = anyVar; // string 타입의 변수에도 any 타입 값을 할당할 수 있다.
```

## unknown

- 어떤 타입의 값이든 다 저장할 수 있는 타입
- any와 비슷해 보이지만, any보다 안전한 타입이다.
  - any는 어떤 타입의 변수에든 할당할 수 있다.
  - unknown은 어떤 타입의 **변수**에도 저장할 수 없다.
- unknown 타입의 값은 어떤 연산에도 참여할 수 없고, 어떤 메서드도 사용할 수 없다.
- 오직 값을 저장하는 행위만 할 수 있다.

```ts
let unknownVar: unknown;

unknownVar = ""; // 어떤 타입 값이든 저장 가능
unknownVar = {};
unknownVar = 1;
```

```ts
let unknownVar: unknown;
let num: number = 10;

unknownVar = 1;
num = unknownVar; // 오류 => 어떤 타입의 변수에도 저장 불가능
```

```ts
let unknownVar: unknown;

unknownVar * 2; // 오류 => 어떤 메서드도 사용할 수 없다.
```

- 만약 unknown 타입의 값을 특정 타입의 값처럼 취급하고 연산을 수행하고 싶다면, 조건문을 이용하면 된다.

```ts
if (typeof unknownVar === "number") {
  // unknownVar의 값이 number 타입이라면
  unknownVar * 2;
}
```

## void

- 아무런 값도 없음을 의미하는 타입
- 보통 아무런 값도 반환하지 **않는** 함수의 반환값 타입을 정의할 때 사용한다.
- 변수의 타입으로도 사용할 수 있지만, void 타입의 변수에는 undefined만 담을 수 있다.
  - tsconfig.json에 `strickNullChecks` 옵션을 `false`로 설정하면 null 값도 담을 수 있다.

```ts
function func(): void {
  console.log("hello");
  // 반환값이 없다. => void 타입
}
```

```ts
let a: void;
a = undefined;
a = null; // strickNullChecks: false일 경우에만 가능
```

## never

- 불가능을 의미하는 타입
- 보통 함수가 어떠한 값도 반환할 수 **없는** 상황일 때 사용한다.
  - 무한루프 => 아무런 값도 반환할 수 없다. => "불가능"
  - 의도적으로 오류를 발생시키는 함수 `throw new Error();`

```ts
// 무한루프
function func1(): never {
  while (true) {}
}

// 의도적으로 오류를 발생시키는 함수
function func2(): never {
  throw new Error();
}
```

<br/>

**참고자료**

- https://ts.winterlood.com/41c52e6a-ad79-4b6e-b87b-909400f161fe
- https://ts.winterlood.com/2fc094af-7fe4-46d4-8c24-bb0596172b2e
