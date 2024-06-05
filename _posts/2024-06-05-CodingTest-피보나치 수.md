---
title: "[Lv2] 피보나치 수"
excerpt: "프로그래머스 Lv2 피보나치 수"

categories:
  - CodingTest
tags:
  - [JavaScript, Programmers, 피보나치 수]

permalink: /JavaScript/Programmers2/

toc: true
toc_sticky: true

date: 2024-06-05
last_modified_at: 2024-06-05
---

# [Lv2] 피보나치 수

## 문제

피보나치 수는 F(0) = 0, F(1) = 1일 때, 1 이상의 n에 대하여 F(n) = F(n-1) + F(n-2) 가 적용되는 수 입니다.

예를들어

- F(2) = F(0) + F(1) = 0 + 1 = 1
- F(3) = F(1) + F(2) = 1 + 1 = 2
- F(4) = F(2) + F(3) = 1 + 2 = 3
- F(5) = F(3) + F(4) = 2 + 3 = 5
  와 같이 이어집니다.

2 이상의 n이 입력되었을 때, n번째 피보나치 수를 1234567으로 나눈 나머지를 리턴하는 함수, solution을 완성해 주세요.

제한 사항
n은 2 이상 100,000 이하인 자연수입니다.

## 제출 답안 (오답)

```js
function solution(n) {
  let fibonacci = [0, 1];
  for (let i = 2; i <= n; i++) {
    fibonacci[i] = fibonacci[i - 1] + fibonacci[i - 2];
  }
  return fibonacci[n] % 1234567;
}
```

- fibonacci 배열을 사용해서 피보나치 수열을 저장한다.
- 마지막 fibonacci[n] 값을 1234567로 나누어 반환한다.

## 오답인 이유

- 메모리 사용량이 커서 **런타임 에러가 발생**한다.
  - `fibonacci(n-1)+fibonacci(n-2)`가 반복되기 때문

## 정답 풀이

```js
function solution(n) {
  let a = 0,
    b = 1,
    temp;
  for (let i = 2; i <= n; i++) {
    temp = (a + b) % 1234567;
    a = b;
    b = temp;
  }
  return temp;
}
```

- **동적 계획법**으로 접근하여 메모리 초과 사용 문제를 해결한다.

  - **동적 계획법**: 문제를 하위 문제로 나누고, 하위 문제들의 결과를 저장하여 동일한 계산을 반복하지 않도록 하는 기법
  - 기존 방식에서 반복한 `F(n-1)+F(n-2)` 과정을 피하기 위해 중간 결과들을 변수에 저장한다.

<br/>

- a, b는 피보나치 수열의 첫 두 항을 나타낸다.
  - a는 F(0)=0, b는 F(1)=1을 저장한다.
- temp는 두 변수의 합을 저장하기 위한 변수이다.
  - a와 b값을 더한 후 1234567로 나눈 나머지를 temp에 저장한다.
  - 이는 계산된 값이 너무 커지는 것을 방지한다.
- `a = b`를 통해 이전의 b값을 a값으로 갱신한다.
- `b = temp`를 통해 이전의 합을 현재 값으로 갱신한다.
