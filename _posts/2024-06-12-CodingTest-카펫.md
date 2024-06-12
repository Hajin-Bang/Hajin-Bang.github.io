---
title: "[Lv2] 카펫"
excerpt: "프로그래머스 Lv2 카펫"

categories:
  - CodingTest
tags:
  - [JavaScript, Programmers, 카펫]

permalink: /JavaScript/Programmers4/

toc: true
toc_sticky: true

date: 2024-06-12
last_modified_at: 2024-06-12
---

# [Lv2] 카펫

## 문제

Leo는 카펫을 사러 갔다가 아래 그림과 같이 중앙에는 노란색으로 칠해져 있고 테두리 1줄은 갈색으로 칠해져 있는 격자 모양 카펫을 봤습니다.

Leo는 집으로 돌아와서 아까 본 카펫의 노란색과 갈색으로 색칠된 격자의 개수는 기억했지만, 전체 카펫의 크기는 기억하지 못했습니다.

Leo가 본 카펫에서 갈색 격자의 수 brown, 노란색 격자의 수 yellow가 매개변수로 주어질 때 카펫의 가로, 세로 크기를 순서대로 배열에 담아 return 하도록 solution 함수를 작성해주세요.

제한사항

- 갈색 격자의 수 brown은 8 이상 5,000 이하인 자연수입니다.
- 노란색 격자의 수 yellow는 1 이상 2,000,000 이하인 자연수입니다.
- 카펫의 가로 길이는 세로 길이와 같거나, 세로 길이보다 깁니다.

## 제출 답안

```js
function solution(brown, yellow) {
  for (let i = 1; i <= Math.sqrt(yellow); i++) {
    if (yellow % i === 0) {
      let width = yellow / i;
      let length = i;
      if ((width + 2) * (length + 2) === brown + yellow) {
        return [width + 2, length + 2];
      }
    }
  }
}
```

- **완전탐색** 알고리즘 문제

  - **완전탐색**: 가능한 모든 경우의 수를 모두 탐색하여 정답을 찾는 방법
    - 모든 경우의 수를 탐색해야 하는 경우
    - 문제의 규모가 작은 경우
    - 명확한 제약 조건이 있는 경우
  - 이 문제에서는 약수를 찾고 약수의 모든 조합을 고려해야하므로 완전탐색을 사용해야한다.

<br/>

- yellow의 약수를 찾는다.
- 각 약수 쌍에 대해 width(가로)와 length(세로)를 계산한다.
- `(width + 2) * (length + 2)`가 `brown + yellow`와 같은지 확인한다.
- 조건이 맞으면 `[width + 2, length + 2]`를 반환한다.

<br/>

- `Math.sqrt()`: 제곱근 계산
