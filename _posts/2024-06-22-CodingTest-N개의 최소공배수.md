---
title: "[Lv2] N개의 최소공배수"
excerpt: "프로그래머스 Lv2 N개의 최소공배수"

categories:
  - CodingTest
tags:
  - [JavaScript, Programmers, N개의 최소공배수]

permalink: /JavaScript/Programmers7/

toc: true
toc_sticky: true

date: 2024-06-22
last_modified_at: 2024-06-22
---

# [Lv2] N개의 최소공배수

## 문제

두 수의 최소공배수(Least Common Multiple)란 입력된 두 수의 배수 중 공통이 되는 가장 작은 숫자를 의미합니다. 예를 들어 2와 7의 최소공배수는 14가 됩니다. 정의를 확장해서, n개의 수의 최소공배수는 n 개의 수들의 배수 중 공통이 되는 가장 작은 숫자가 됩니다. n개의 숫자를 담은 배열 arr이 입력되었을 때 이 수들의 최소공배수를 반환하는 함수, solution을 완성해 주세요.

제한 사항

- arr은 길이 1이상, 15이하인 배열입니다.
- arr의 원소는 100 이하인 자연수입니다.

## 제출 답안

```js
function gcd(a, b) {
  if (b === 0) {
    return a;
  } else if (a % b === 0) {
    return b;
  } else {
    return gcd(b, a % b);
  }
}

function lcm(a, b) {
  return (a * b) / gcd(a, b);
}

function solution(arr) {
  let answer = 1;
  for (let i = 0; i < arr.length; i++) {
    answer = lcm(answer, arr[i]);
  }
  return answer;
}
```

## 알아야 할 개념

- 최대공약수를 구하는 방법: `유클리드 호제법`
- 최소공배수를 구하는 방법: `(두 수의 곱) / 최대공약수`

> ### 유클리드 호제법이란?
>
> 2개의 자연수의 최대공약수를 구하는 알고리즘으로, 두 수가 서로 상대방 수를 나누어서 원하는 수를 얻게 된다. <br/>
> a,b에 대해서 a를 b로 나눈 나머지를 r이라고 하면, a와 b의 최대공약수는 b와 r의 최대공약수와 같다. 이 성질에 따라, b를 r로 나눈 나머지를 구하고, 다시 그 r을 그 나머지로 나눈 나머지를 구하는 과정을 반복하여 나머지가 0이 되었을 때 나누는 수가 a와 b의 최대공약수이다.

## 풀이

- 최대공약수를 구하는 함수 `gcd`

  - b가 0이면 최대공약수는 a
  - `a%b === 0`이면 최대공약수는 b
  - 나누었을 때 나머지가 0이 아니라면 계속해서 b와 `a % b`를 가지고 나머지가 0일 때까지 나눈다.
  - 0이 되게하는 나머지가 최대공약수가 된다.

- 최소공배수를 구하는 함수 `lcm`

  - 두 수의 곱에서 gcd함수를 통해 구한 최대공약수를 나눈다.

- N개의 최소공배수 구하기 (함수 `solution`)
  - answer에는 앞에서부터 구한 두 수의 최소공배수를 담는다.
  - 두 수의 최소공배수 a를 구하고, a와 다른 수의 최소공배수 b를 구하면 b는 곧 세가지 수의 최소공배수가 된다.
  - 이렇게 N개의 최소공배수를 구할 수 있다.

<br/>
<참고>

- https://velog.io/@jan/%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%A8%B8%EC%8A%A4-N%EA%B0%9C%EC%9D%98-%EC%B5%9C%EC%86%8C%EA%B3%B5%EB%B0%B0%EC%88%98-JavaScript
- https://ko.wikipedia.org/wiki/%EC%9C%A0%ED%81%B4%EB%A6%AC%EB%93%9C_%ED%98%B8%EC%A0%9C%EB%B2%95
