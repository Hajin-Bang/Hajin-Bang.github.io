---
title: "깊이 우선 탐색(DFS)"
excerpt: "깊이 우선 탐색(DFS) 알고리즘에 대하여"

categories:
  - Algorithm
tags:
  - [DFS, Algorithm]

permalink: /Algorithm/DFS/

toc: true
toc_sticky: true

date: 2024-02-27
last_modified_at: 2024-02-27
---

# 깊이 우선 탐색(DFS)

## 깊이 우선 탐색(DFS)

- 깊이를 우선으로 탐색하는 알고리즘 (정점의 자식을 먼저 탐색)
- 모든 노드에 대한 방문 확인을 탐색하는 데에 최적인 알고리즘
- BFS보다 속도는 느리지만, 더 간단함
- 방문한 노드에 대해서 반드시 확인해야함

## 깊이 우선 탐색(DFS) 구현하기

### 1. 재귀 함수를 활용한 구현

```js
const Graph = {
  A: ["B", "C"],
  B: ["A", "C", "D"],
  C: ["A", "B", "D"],
  D: ["B", "C"],
};

const visited = [];
const visitedNode = [];

function dfs(startNode) {
  if (!visitedNode.includes(startNode)) {
    visited[startNode] = true;
    visitedNode.push(startNode);
  }
  for (let curNode of Graph[startNode]) {
    if (!visited[curNode]) {
      dfs(curNode);
    }
  }
}

dfs("A");
console.log(visitedNode); // ['A', 'B', 'C', 'D']
```

### 2. 스택(Stack)을 활용한 구현

```js
function dfs(graph, start, visited) {
  const stack = [];
  stack.push(start);

  while (stack.length) {
    let v = stack.pop();
    if (!visited[v]) {
      console.log(v);
      visited[v] = true;

      for (let node of graph[v]) {
        if (!visited[node]) {
          stack.push(node);
        }
      }
    }
  }
}

const graph = [[1, 2, 4], [0, 5], [0, 5], [4], [0, 3], [1, 2]];
const visited = Array(7).fill(false);

dfs(graph, 0, visited);
```

<br/>

**참고자료**

- https://uic11.tistory.com/entry/%EA%B9%8A%EC%9D%B4-%EC%9A%B0%EC%84%A0-%ED%83%90%EC%83%89Depth-First-Search%EC%9D%84-%EC%95%8C%EC%95%84%EB%B3%B4%EC%9E%90-featJS

- https://chamdom.blog/dfs-using-js/
