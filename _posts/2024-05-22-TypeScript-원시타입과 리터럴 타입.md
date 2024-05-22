---
title: "원시타입과 리터럴 타입"
excerpt: "TypeScript의 원시 타입과 리터럴 타입"

categories:
  - TypeScript
tags:
  - [TypeScript, 원시 타입, 리터럴 타입]

permalink: /TypeScript/원시타입과 리터럴 타입/

toc: true
toc_sticky: true

date: 2024-5-23
last_modified_at: 2024-05-23
---

# TypeScript

## 원시타입

- 동시에 한 개의 값만 저장할 수 있는 타입
- number, string, boolean 등

### number

- 숫자를 의미하는 모든 값을 포함하는 타입
- 단순 정수 뿐만 아니라 소수, 음수, Infinity, NaN 등의 특수한 숫자 모두를 포함한다.
- number 타입으로 정의한 변수에 number 타입의 값이 사용할 수 없는 메서드를 적용할 경우 오류가 발생한다.
  - ex. `toUpperCase()`

```ts
let num1: number = 123;
let num2: number = -123;
let num3: number = 0.123;
let num4: number = -0.123;
let num5: number = Infinity;
let num6: number = -Infinity;
let num7: number = NaN;
```

> 변수의 이름 뒤에 콜론(`: `)을 붙여 정의하는 문법을 `타입 주석` 또는 `타입 어노테이션`이라고 부른다.

### string

- 문자열을 의미하는 타입
- 쌍따옴표, 작은 따옴표, 백틱, 템플릿 리터럴로 만든 모든 문자열을 포함한다.

```ts
let str1: string = "hello";
let str2: string = "hello";
let str3: string = `hello`;
let str4: string = `hello ${str1}`;
```

### boolean

- 참과 거짓을 저장하는 타입
- true와 false만 해당된다.

```ts
let bool1: boolean = true;
let bool2: boolean = false;
```

### null

- null 값만 포함하는 타입

```ts
let null : null = null;
```

### undefined

- undefined만 포함하는 타임

```ts
let unde1: undefined = undefined;
```

> **💡null 값을 임시값으로 사용하고 싶을 경우** > </br>
>
> `let num: number = null`과 같이 null이 아닌 다른 타입의 값에 임시로 null 값을 넣고 싶은 상황이 생길 수 있다.
> 이럴 경우 tsconfig.json의 `strictNullChecks`옵션을 `false`로 설정하면 된다. </br>
> 이는 엄격한 null 검사 옵션으로, null 타입 외 타입의 변수에 null 값을 할당하는 것을 허락할지 결정하는 옵션이다.

## 리터럴 타입

- 딱 하나의 값만 포함하는 타입
- 값 하나를 설정하면, 설정한 값 외의 다른 값을 저장할 수 없게 된다.
- number, string, boolean 타입의 값 모두 리터럴 타입으로 만들 수 있다.

```ts
let numA: 10 = 10; // 10 외의 다른 값 저장 불가
let strA: "hello" = "hello"; // "hello" 외의 다른 값 저장 불가
let boolA: true = true; // true 외의 다른 값 저장 불가
```

  <br/>

**참고자료**

- https://ts.winterlood.com/3cb27a06-78ac-499d-9270-2ebabe8c769c
