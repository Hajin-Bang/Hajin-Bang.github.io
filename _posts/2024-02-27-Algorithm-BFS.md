---
title: "너비 우선 탐색(BFS)"
excerpt: "너비 우선 탐색(BFS) 알고리즘에 대하여"

categories:
  - Algorithm
tags:
  - [BFS, Algorithm]

permalink: /Algorithm/BFS/

toc: true
toc_sticky: true

date: 2024-02-27
last_modified_at: 2024-02-27
---

# 너비 우선 탐색(BFS)

## 너비 우선 탐색(BFS)

- 너비를 우선적으로 탐색하는 알고리즘
  - 현재 위치에서 갈 수 있는 가장 가까운 노드를 우선으로 탐색
- 두 지점 사이의 최단 거리를 구하거나 경로를 찾는데에 최적화됨

## 너비 우선 탐색(BFS) 구현하기

### 큐(Queue)를 이용한 구현

#### 1. 배열을 사용

```js
const Graph = {
  A: ["B", "C"],
  B: ["A", "C", "D"],
  C: ["A", "B", "D"],
  D: ["B", "C"],
};

function bfs(startNode) {
  const Queue = [];
  const visitedNode = [];

  Queue.push(startNode);
  visitedNode.push(startNode);
  while (Queue.length > 0) {
    const curNode = Queue.shift();
    for (let nearNode of Graph[curNode]) {
      if (!visitedNode.includes(nearNode)) {
        Queue.push(nearNode);
        visitedNode.push(nearNode);
      }
    }
  }
  return;
}
console.log(bfs("A")); // ['A', 'B', 'C', 'D']
```

#### 2. 큐(Queue) 클래스를 직접 구현

```js
// 큐 구현
class Queue {
  constructor() {
    this.store = {};
    this.front = 0;
    this.rear = 0;
  }

  size() {
    if (this.store[this.rear] === undefined) {
      return 0;
    } else {
      return this.rear - this.front + 1;
    }
  }

  push(value) {
    if (this.size() === 0) {
      this.store["0"] = value;
    } else {
      this.rear += 1;
      this.store[this.rear] = value;
    }
  }

  popleft() {
    let temp;
    if (this.front === this.rear) {
      temp = this.store[this.front];
      delete this.store[this.front];
      this.front = 0;
      this.rear = 0;
      return temp;
    } else {
      temp = this.store[this.front];
      delete this.store[this.front];
      this.front += 1;
      return temp;
    }
  }
}

// BFS 구현
function BFS(graph, start, visited) {
  const queue = new Queue();
  queue.push(start);
  visited[start] = true;

  while (queue.size()) {
    const v = queue.popleft();
    console.log(v);

    for (const node of graph[v]) {
      if (!visited[node]) {
        queue.push(node);
        visited[node] = true;
      }
    }
  }
}

const graph = [[1, 2, 4], [0, 5], [0, 5], [4], [0, 3], [1, 2]];
const visited = Array(6).fill(false);
BFS(graph, 0, visited);
// 0 1 2 4 5 3
```

<br/>

**참고자료**

- https://uic11.tistory.com/entry/%EB%84%88%EB%B9%84-%EC%9A%B0%EC%84%A0-%ED%83%90%EC%83%89Breadth-First-Search%EC%9D%84-%EC%95%8C%EC%95%84%EB%B3%B4%EC%9E%90-featJS

- https://chamdom.blog/bfs-using-js/
