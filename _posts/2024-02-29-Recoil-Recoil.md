---
title: "Recoil"
excerpt: "React의 상태 관리 라이브러리"

categories:
  - React
tags:
  - [Recoil, React]

permalink: /React/Recoil/

toc: true
toc_sticky: true

date: 2024-02-29
last_modified_at: 2024-02-29
---

# Recoil

**Recoil**은 Facebook에서 개발한 상태 관리 라이브러리이다. <br/>
React에는 `redux`, `mobx` 등 여러가지 상태 관리 라이브러리가 존재한다. 그 중에서도 어떤 이유로 `Recoil`을 사용하고, 어떻게 사용하는지 알아보자.

## Recoil의 장점

- 직관적고 간단한 구조를 가진다.
- 중앙 집중화된 상태 관리를 지원하여, 상태를 관리하는 것이 용이하다.
- 비교적 간단한 세팅으로 러닝커브가 낮다.

## 초기 세팅

`npm install recoil`을 통해 recoil을 설치한 후에, 최상위(루트) 컴포넌트를 `RecoilRoot`로 감싸주어야한다.

```js
import React from "react";
import { RecoilRoot } from "recoil";

function App() {
  return (
    <RecoilRoot>
      <Main />
    </RecoilRoot>
  );
}
```

## 주요 개념

### Atom

**Atom**은 하나의 상태로, 어떤 컴포넌트에서나 읽고 쓸 수 있다. atom값을 변경하면 그것을 구독하고 있는 컴포넌트들이 모두 다시 렌더링된다.

```js
import { atom } from "recoil";
export const age = atom({
  key: "age", // key값
  default: 0, // 초기값
});
```

atom은 고유의 **key값**과 **초기값**을 가진다. 컴포넌트에서 사용할 때, 이 key값을 이용해 식별한다. <br/>
**atom은 `useRecoilState`를 통해 접근 가능하다.**

> **key** <br/>
> atom의 고유값
>
> **default** <br/>
> 초기값

### Selectors

**Selector**는 atom이나 다른 select를 기반으로 파생된 상태를 만드는 순수 함수이다. 상위의 atoms 또는 selects가 업데이트되면 하위의 selector 함수도 다시 실행된다.

```js
import { selector } from "recoil";
import { age } from "...";

export const isChild = selector({
  key: "childage",
  get: ({ get }) => {
    const state = get(age);
    return state < 10;
  },
});
```

selector 함수에서는 atom과 마찬가지로 고유의 **key값**이 필요하며, **get 속성**을 통해 사용할 값을 반환한다. get을 이용하여 atom과 다른 selectors에 접근할 수 있다. <br/>
**selector는 `useRecoilState`를 통해 접근 가능하다.**

메서드로는 **set 속성**을 사용할 수도 있는데, set을 설정하게 되면 쓰기 가능한 모드로 변경된다. 이는 콜백객체, 새로운 값 2가지를 각각 매개변수로 받는다.

```js
import { selector } from "recoil";
import { age } from "...";

export const isChild = selector({
  key: "childage",
  get: ({ get }) => {
    const state = get(age);
    return state < 10;
  },
  set: ({ set }, newValue) => set(age, newValue),
});
```

> **key** <br/>
> selector의 고유값
>
> **get** <br/>
> 데이터를 가공하는 함수
>
> **set** <br/>
> 쓰기 가능한 객체를 반환하는 함수 <br/>
> (객체, 새로운 값) <br/>
> 필수 값은 아님 <br/>

## Hooks

#### `useRecoilState`

전역 상태의 현재 상태. 값과 그 값을 업데이트하는 함수를 반환한다.

#### `useRecoilValue`

전역 상태의 현재 상태값을 반환한다.(상태를 설정하지 않고 값만 가져온다.)

#### `useSetRecoilState`

전역 상태의 setter 함수 즉, 상태값을 업데이트하는 함수를 반환한다. (값을 불러오지 않고 상태를 설정한다.)

#### `useResetRecoilState`

전역 상태를 default(초기값)으로 reset한다.

```js
import { atom } from "recoil";

const counterState = atom({
  key: "counter",
  default: 0,
});

export { counter };
```

```js
import { counter } from "...";
import {
  useRecoilState,
  useRecoilValue,
  useSetRecoilState,
  useResetRecoilState,
} from "recoil";

function Counter() {
  const [count, setCount] = useRecoilState(countState); // countState의 값, 상태함수 반환
  const countValue = useRecoilValue(countState); // countState의 값만 반환
  const setCountState = useSetRecoilState(countState); // 상태함수(값을 변경하는 함수)만 반환
  const resetCount = useResetRecoilState(countState); // 상태값을 default 값으로 초기화

  return <div>...</div>;
}

export default Counter;
```

<br/>

**참고자료**

- https://recoiljs.org/ko/docs/introduction/getting-started
