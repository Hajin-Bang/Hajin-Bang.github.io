---
title: "[Lv2] 구명보트"
excerpt: "프로그래머스 Lv2 구명보트"

categories:
  - CodingTest
tags:
  - [JavaScript, Programmers, 구명보트]

permalink: /JavaScript/Programmers6/

toc: true
toc_sticky: true

date: 2024-06-19
last_modified_at: 2024-06-19
---

# [Lv2] 구명보트

## 문제

무인도에 갇힌 사람들을 구명보트를 이용하여 구출하려고 합니다. 구명보트는 작아서 한 번에 최대 2명씩 밖에 탈 수 없고, 무게 제한도 있습니다.

예를 들어, 사람들의 몸무게가 [70kg, 50kg, 80kg, 50kg]이고 구명보트의 무게 제한이 100kg이라면 2번째 사람과 4번째 사람은 같이 탈 수 있지만 1번째 사람과 3번째 사람의 무게의 합은 150kg이므로 구명보트의 무게 제한을 초과하여 같이 탈 수 없습니다.

구명보트를 최대한 적게 사용하여 모든 사람을 구출하려고 합니다.

사람들의 몸무게를 담은 배열 people과 구명보트의 무게 제한 limit가 매개변수로 주어질 때, 모든 사람을 구출하기 위해 필요한 구명보트 개수의 최솟값을 return 하도록 solution 함수를 작성해주세요.

제한사항

- 무인도에 갇힌 사람은 1명 이상 50,000명 이하입니다.
- 각 사람의 몸무게는 40kg 이상 240kg 이하입니다.
- 구명보트의 무게 제한은 40kg 이상 240kg 이하입니다.
- 구명보트의 무게 제한은 항상 사람들의 몸무게 중 최댓값보다 크게 주어지므로 사람들을 구출할 수 없는 경우는 없습니다.

## 제출 답안

```js
function solution(people, limit) {
  let count = 0;
  let len = people.length;
  people.sort((a, b) => a - b);
  let start = 0;
  let end = len - 1;
  while (start <= end) {
    if (people[start] + people[end] <= limit) {
      start++;
      end--;
    } else {
      end--;
    }
    count++;
  }
  return count;
}
```

- **그리디(탐욕법)** 알고리즘 문제

  - **그리디**: 현재 상황에서 가장 최적의 선택을 하는 방법
  - 이 문제에서는 매 순간 최적의 선택을 통해 최선이 되도록 문제를 구성하는 것이 중요한 문제이다.
    - 사람들의 몸무게를 오름차순으로 정렬
    - 가장 가벼운 사람과 가장 무거운 사람을 태우도록 고려
    - 이 과정을 반복해서 무게 합이 제한 이하인지 확인한다.
