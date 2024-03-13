---
title: "Axios"
excerpt: "node.js 와 브라우저를 위한 http통신 라이브러리"

categories:
  - JavaScript
tags:
  - [Axios, JavaScript]

permalink: /JavaScript/Axios/

toc: true
toc_sticky: true

date: 2024-03-13
last_modified_at: 2024-03-13
---

# Axios

**Axios**는 node.js와 브라우저를 위한 Http 통신 라이브러리이다. <br/>
Http 통신 라이브러리 중에는 jQuery Ajax, fetch 등이 있다.

> **왜 Axios를 많이 사용할까?**
>
> - 유연성과 호환성: 브라우저와 Node.js 환경 모두에서 사용할 수 있으며, 다양한 요구사항에 맞춰 사용할 수 있는 유연성을 제공한다.
> - 기능성: 자동 JSON 반환, 에러 처리의 용이성, 요청 취소 등 Axios만의 고급 기능이 있다.
> - 간결한 코드: Promise 기반으로 작동하며, async/await와의 호환으로 비동기 코드를 간결하고 이해하기 쉽게 작성할 수 있다.

## Axios vs fetch vs jQuery Ajax

**1.Axios**
(장점)

- Promise 기반으로 작동하며, async/await 사용과 함께 비동기 코드 작성을 지원한다.
- 자동으로 JSON 데이터를 변환한다.
- catch에 걸렸을 때 console에 자동으로 로그가 삽입된다.
  (단점)
- 외부 라이브러리이므로 프로젝트에 추가해야한다.
- 작은 단일 페이지 어플리케이션에서는 과도한 기능일 수 있다.

**2. fetch**
(장점)

- 자바스크립트 내장 라이브러리로, import 하지 않고 사용 가능하다.
- 사용법이 간단하며, 간단한 요청에서는 불필요한 설정 없이 사용할 수 있다.
  (단점)
- 응답 데이터가 바로 넘어오지 않아 JSON으로 파싱해야한다.
- HTTP 에러(404,500 등)를 자동으로 걸러내지 못한다.
  - 에러 처리가 직관적이지 못하다.

**3. jQuery Ajax**
(장점)

- jQuery를 통해 쉽게 구현이 가능하다.
- 크로스 브라우징 이슈를 자체적으로 처리한다.
  (단점)
- 현대 웹 개발에서는 대부분의 브라우저 API가 표준화되고 개선되면서 jQuery의 필요성이 감소했다.

## Axios 사용법

### Axios의 메서드

- GET: 데이터 조회, `axios.get(url[, config])`
- POST: 데이터 등록 및 전송, `axios.post(url, data[, config])`
- PUT: 데이터 수정, `axios.put(url, data[, config])`
- DELETE: 데이터 삭제, `axios.delete(url[, config])`

### Axios 설치하기

`npm install axios`
외부 라이브러리이므로 설치 후 사용 가능하다.

### GET 요청

기본 사용 방법

```js
const axios = require('axios');

axios.get('/user?ID=12345')
    .then(function(response) {
    console.log(response);
    })
    .catch(function(error) => {
    console.log(error);
})
```

async/await와 함께 사용하는 방법

```js
async function fetchData() {
  try {
    const response = await axios.get("/user?ID=12345");
    console.log(response.data);
  } catch (error) {
    console.error("Error:", error);
  }
}

fetchData();
```

### POST 요청

```js
axios
  .post("https://api.example.com/items", {
    name: "New Item",
    category: "Books",
  })
  .then((response) => {
    console.log(response);
  })
  .catch((error) => {
    console.error(error);
  });
```

### PUT 요청

```js
axios
  .put("https://api.example.com/items/1", {
    name: "Updated Item",
    category: "Electronics",
  })
  .then((response) => {
    console.log(response);
  })
  .catch((error) => {
    console.error(error);
  });
```

### DELETE 요청

```js
axios
  .delete("https://api.example.com/items/1")
  .then((response) => {
    console.log("Deleted successfully");
  })
  .catch((error) => {
    console.error(error);
  });
```

### 멀티 요청

여러 개의 요청을 동시 수행할 경우 `axios.all()` 메서드를 사용합니다.

```js
function getUserAccount() {
  return axios.get("/user/12345");
}

function getUserPermissions() {
  return axios.get("/user/12345/permissions");
}

axios
  .all([getUserAccount(), getUserPermissions()])
  .then(axios.spread(function (acct, perms) {}));
```

<br/>

**참고자료**

- https://itprogramming119.tistory.com/entry/React-axios%EB%A5%BC-%EC%82%AC%EC%9A%A9%ED%95%98%EB%8A%94-%EC%9D%B4%EC%9C%A0-vs-fetch
