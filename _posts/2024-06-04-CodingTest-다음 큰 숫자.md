---
title: "[Lv2] 다음 큰 숫자"
excerpt: "프로그래머스 Lv2 다음 큰 숫자"

categories:
  - CodingTest
tags:
  - [JavaScript, Programmers, 다음 큰 숫자]

permalink: /JavaScript/Programmers1/

toc: true
toc_sticky: true

date: 2024-06-04
last_modified_at: 2024-06-04
---

# [Lv2] 다음 큰 숫자

## 문제

자연수 n이 주어졌을 때, n의 다음 큰 숫자는 다음과 같이 정의 합니다.

- 조건 1. n의 다음 큰 숫자는 n보다 큰 자연수 입니다.
- 조건 2. n의 다음 큰 숫자와 n은 2진수로 변환했을 때 1의 갯수가 같습니다.
- 조건 3. n의 다음 큰 숫자는 조건 1, 2를 만족하는 수 중 가장 작은 수 입니다.
  예를 들어서 78(1001110)의 다음 큰 숫자는 83(1010011)입니다.

자연수 n이 매개변수로 주어질 때, n의 다음 큰 숫자를 return 하는 solution 함수를 완성해주세요.

제한 사항
n은 1,000,000 이하의 자연수 입니다.

## 제출 답안

```js
function count(n) {
  binary = n.toString(2);
  let countOne = 0;
  for (let i = 0; i < binary.length; i++) {
    if (binary[i] == "1") countOne++;
  }
  return countOne;
}

function solution(n) {
  testNum = n;
  while (true) {
    testNum++;
    if (count(testNum) == count(n)) return testNum;
  }
}
```

- `count(n)`: 자연수 n을 2진수로 변환한 후, 1의 개수를 세어 반환하는 함수
- `solution(n)`: 입력받은 n에서 1씩 늘려가며 count(n)으로 1의 개수를 세고, n의 1 개수와 동일한 수를 반환하는 함수

<br/>

- `toString(2)`: 2진수로 변환
- `while(true)`: `while(조건문)`은 조건문이 참일 경우 계속 반복되는 반복문이므로, true값을 넣으면 계속 반복되는 반복문이 된다.

## 다른 풀이

```js
function solution(n) {
  let oneNum = n.toString(2).split("1").length - 1;
  while (true) {
    n++;
    if (n.toString(2).split("1").length - 1 == oneNum) return n;
  }
}
```

- 1을 기준으로 2진수 문자를 잘라 배열에 저장한다.
  - 예를 들어 값이 101일 경우 배열은 ["", "0", ""]이므로 length는 3이 된다.
  - 101010 => `split("1")` => ["", "0", "0", "0"]
  - 1010101 => `split("1")` => ["", "0", "0", "0", ""]
- 즉 1의 개수는 length - 1

<br/>

- `split("")`: 문자열을 일정한 구분자로 잘라서 배열로 저장
  - `split("1")`: 1을 기준으로 잘라서 배열에 저장
  - `split()`: 문자열 전체를 length 1인 배열에 담아서 저장
  - `split(" ")`: 스페이스(공백)을 기준으로 단어를 잘라서 저장
  - `split("")`: 공백을 포함하여 각각 잘라서 배열에 저장
  - `split(",")`: ,를 기준으로 잘라서 배열에 저장
