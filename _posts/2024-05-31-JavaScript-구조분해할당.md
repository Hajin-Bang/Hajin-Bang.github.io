---
title: "구조 분해 할당"
excerpt: ""

categories:
  - JavaScript
tags:
  - [JavaScript, 구조 분해 할당]

permalink: /JavaScript/구조_분해_할당/

toc: true
toc_sticky: true

date: 2024-5-31
last_modified_at: 2024-05-31
---

# 구조 분해 할당

- 배열이나 객체의 구조를 분해해서 할당하는 문법
  - 요소를 해체해 개별 변수에 그 값을 담을 때 사용

## 배열의 구조 분해 할당

- 저장된 요솟값을 변수 선언과 동시에 순서대로 할당한다.
  - 선언하지 않고 바로 할당도 가능
- 배열의 길이보다 더 많은 변수에 배열 요소의 값을 할당하려 하면, 남은 변수에는 undefined가 할당된다.

```ts
let arr = [1, 2, 3];

let one = arr[0];
let two = arr[1];
let three = arr[2];

// 위와 같은 과정을 구조 분해 할당하면 아래와 같이 간결하게 작성할 수 있다.
let arr = [1, 2, 3];
let [one, two, three] = arr;

// 별도로 선언하지 않고 바로 할당하기
let [one, two, three] = [1, 2, 3];
console.log(one); // 1
```

## 객체의 구조 분해 할당

- 데이터 저장 순서가 아니라 key를 기준으로 한다.

```ts
let person = {
  name: "방하진",
  age: 25,
  location: "서울",
};

let { name, age, location } = person;
console.log(name, age, location); // 방하진 25 서울
```

<br/>

**참고자료**

- https://reactjs.winterlood.com/85ffb815-e3cd-4c97-b00f-0dd96d22b65b
