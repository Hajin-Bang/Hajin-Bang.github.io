---
title: "Type Alias와 Index Signature"
excerpt: "TypeScript의 타입 별칭과 인덱스 시그니처"

categories:
  - TypeScript
tags:
  - [TypeScript, Type Alias, Index Signature]

permalink: /TypeScript/Type Alias와 Index Signature/

toc: true
toc_sticky: true

date: 2024-5-23
last_modified_at: 2024-05-23
---

# Type Alias와 Index Signature

## Type Alias

- 타입 별칭을 이용하면 변수를 선언하듯 타입을 별도로 정의할 수 있다.
- `type 타입이름 = 타입`의 형태로 정의한다.
- 타입 별칭을 사용할 때는 `: 타입별칭`으로 사용한다.
- 동일한 스코프에 동일한 이름의 타입 별칭을 선언할 수는 없다.
  - 스코프가 다르다면 중복된 이름으로 선언할 수 있다.
- 타입의 중복 선언을 줄일 수 있다.

```ts
// 타입 별칭
type User = {
  id: number;
  name: string;
  nickname: string;
  location: string;
};

// 타입 별칭 사용
let user1: User = {
  id: 1,
  name: "hajin",
  nickname: "bang",
  location: "Seoul",
};

let user2: Uesr = {
  id: 2,
  name: "haha",
  nickname: "bangbang",
  location: "Incheon",
};
```

## Index Signature

- 인덱스 시그니처는 객체 타입을 유연하게 정의할 수 있도록 돕는 문법이다.
- key의 타입, value의 타입을 지정하여 중복된 타입 선언을 줄일 수 있다.
- `[key: key의 타입]: value의 타입`으로 정의한다.

```ts
type NameId = {
  [key: string]: number; // key가 string 타입이고 value가 number 타입인 모든 프로퍼티를 포함
};

let nameId: NameId = {
  BangHajin: 1,
  BangHaHa: 2,
  Bangjinjin: 3,
};
// 이렇게 하면 key가 string, value가 number인 프로퍼티를 하나하나 명시할 필요가 없다.
```

- 반드시 포함해야 하는 프로퍼티가 있다면 직접 명시해도 된다.
- 이렇게 할 경우 인덱스 시그니처의 value 타입과 직접 추가한 프로퍼티의 value 타입이 일치해야 한다.

```ts
type NameId = {
  [key: string]: number;
  BangHajin: number;
  BangHajin: "hajin"; // 오류
};
```

<br/>

**참고자료**

- https://ts.winterlood.com/43888ee0-9227-4a8d-994e-2336ee78bfcf
- https://ts.winterlood.com/1c336fb6-1a90-4076-8de1-b23810a65163
