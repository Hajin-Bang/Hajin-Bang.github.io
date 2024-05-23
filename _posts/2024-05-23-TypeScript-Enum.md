---
title: "Enum"
excerpt: "TypeScript의 열거형(Enum)타입"

categories:
  - TypeScript
tags:
  - [TypeScript, Enum]

permalink: /TypeScript/Enum/

toc: true
toc_sticky: true

date: 2024-5-23
last_modified_at: 2024-05-23
---

# Enum

## Enum

- 열거형 타입
- 여러가지 값들에 각각 이름을 부여해 열거해두고 사용하는 타입
- JavaScript에는 존재하지 않고, TypeScript에서만 사용할 수 있다.
- 여러 값을 숫자로 표기해야할 때 enum을 이용해 보다 직관적으로 관리할 수 있다.

```ts
enum Role {
  ADMIN = 0,
  USER = 1,
  GUEST = 2,
}

const user1 = {
  name: "방하진",
  role: Role.ADMIN, // ADMIN -> 0이 할당
};

const user2 = {
  name: "방방방",
  role: Role.USER, // USER -> 1이 할당
};
```

## Enum의 자동 할당

- enum 멤버에 숫자 값을 직접 할당하지 않아도 0부터 1씩 늘어나는 값으로 자동 할당된다.
- 만약 할당되는 값을 변경하고싶다면, 시작 위치에 값을 직접 할당해주면 된다.
  - 자동으로 다음 멤버에는 할당한 값에서 1씩 증가한 값이 할당된다.
- enum은 컴파일 될 때 다른 타입들처럼 사라지지 않고 JavaScript 객체로 변환된다.
  - 계속 사용할 수 있다.

```ts
enum Role {
  ADMIN, // 아무것도 할당하지 않았을 때 => 0 자동 할당
  USER, // 1 자동 할당
  GUEST, // 2
}
```

```ts
enum Role {
  ADMIN = 10, // 원하는 값을 직접 할당
  USER, // 자동으로 +1된 값 할당 => 11 자동 할당
  GUEST, // 12
}

const user1 = {
  name: "방하진",
  role: Role.GUEST, // 12
};
```

- enum의 멤버에는 문자열 값도 할당할 수 있다.

```ts
enum Role {
  ADMIN = 10, // 원하는 값을 직접 할당
  USER, // 자동으로 +1된 값 할당 => 11 자동 할당
  GUEST, // 12
}

enum Language {
  korean = "ko",
  english = "en",
}

const user1 = {
  name: "방하진",
  role: Role.GUEST, // 12
  language: Language.english, // "en"
};
```

<br/>

**참고자료**

- https://ts.winterlood.com/ed2b0365-72ea-4c3e-b646-7e9e22a472aa
