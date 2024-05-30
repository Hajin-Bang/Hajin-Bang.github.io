---
title: "타입 단언"
excerpt: ""

categories:
  - TypeScript
tags:
  - [TypeScript, 타입 단언]

permalink: /TypeScript/타입_단언/

toc: true
toc_sticky: true

date: 2024-5-30
last_modified_at: 2024-05-30
---

# 타입 단언

- 특정 값을 원하는 타입으로 단언하는 것
- `값 as 타입`의 형태로 단언한다. => `A as B`
  - A가 B의 슈퍼타입이다.
  - A가 B의 서브타입이다.
  - 위 두가지 조건 중 한가지를 반드시 만족해야만 단언할 수 있다.

```ts
let num1 = 10 as never; // never 타입은 모든 타입의 서브타입이다. // 단언 가능
let num2 = 10 as unknown; // unknown 타입은 모든 타입의 슈퍼 타입이다. // 단언 가능
let num3 = 10 as string; // string 타입은 10과 어떤 관계도 맺지 않는다. // 단언 불가능
```

### 다중 단언

- 타입을 다중으로 단언할 수 있다.
- 왼쪽에서 오른쪽으로 단언이 이루어진다.
- 오류가 발생할 확률이 높아지므로 사용을 권장하지 않는다.

```ts
let num3 = 10 as unknown as string;
// number 타입을 unknown 타입으로 단언한다.
// unknown 타입을 string 타입으로 단언한다.
// => unknown이 모든 타입의 슈퍼타입이므로 string 타입으로 단언하는 것이 가능해진다.
```

### const 단언

- 특정 값을 const 타입으로 단언하면 마치 변수를 const로 선언한 것과 비슷하게 타입이 변경된다.

```ts
let num4 = 10 as const; // 상수 타입(number literal)으로 변경된다.
let cat = {
  name: "야옹",
  color: "yellow",
} as const;
// 모든 프로퍼티가 readonly를 갖도록 단언된다.
```

### Non Null 단언

- `값 as 타입` 형태를 따르지 않는 단언
- 값 뒤에 느낌표 `!`를 붙여주면 값이 undefined이거나 null이 **아닐 것**으로 단언할 수 있다.
- 오류가 발생할 수 있으므로 확실한 경우에만 사용해야한다.

```ts
type Post = {
  title: string;
  author?: string; // 선택적 프로퍼티로 정의
};

let post: Post = {
  title: "게시글1",
  author: "방하진",
};

const len: number = post.author!.length;
// author가 undefined이나 null이 아닐 것이라고 단언해준다.
// undefined나 null이라면 length이 적용되지 않아 오류가 발생할 것이다.
// 따라서 그 값이 아니라고 컴퓨터에게 전달하는 것이다.
```

<br/>

**참고자료**

- https://ts.winterlood.com/71f4a577-4340-4994-956d-a7aa47176ffa
