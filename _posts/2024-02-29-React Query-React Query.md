---
title: "React Query"
excerpt: "fetching, caching, 서버 데이터와의 동기화를 지원해주는 라이브러리"

categories:
  - React Query
tags:
  - [React Query, React]

permalink: /React/React-Query/

toc: true
toc_sticky: true

date: 2024-02-29
last_modified_at: 2024-02-29
---

# React Query

React Query는 React에서 서버의 상태를 불러오고, 캐싱하며 지속적으로 동기화하는 작업을 도와주는 라이브러리이다. 조금 더 규격화된 API 요청 방식을 사용하고, useEffect 코드를 줄임으로써 복잡한 코드구조를 개선하기 위해 사용한다.

### 캐싱(Cashing)

동일한 데이터에 대한 반복적인 비동기 데이터 호출을 방지하여 불필요한 데이터 호출을 줄여서 서버 부하를 막는다.

## 초기 세팅

`npm install react-query`를 통해 react-query를 설치한다. 이후 QueryClient를 정의하고, QueryClientProvider한테 전달해준다. 그리고 최상위(루트) 컴포넌트를 `QueryClientProvider`로 감싸주어야한다.

```js
import React from "react";
import { QueyClient, QueryClientProvider } from "react-query";

const queryClient = new QueryClient(); // 쿼리 인스턴스 생성

function App() {
  return (
    <QueryClientProvider client={queryClient}>
      {/*생성한 인스턴스를 넘겨줌 */}
      <Main />
    </QueryClientProvider>
  );
}
```

## useQuery

- 데이터를 `get`하기 위해 사용하는 Hook이다.
- 첫번째 파라미터로 unique key(queryKey), 두번째 파라미터로 호출하고자 하는 함수(queryFn)가 들어간다.
  - `useQuery(키 값, 비동기 함수, options)`
- return 값: api의 성공or실패 여부, 반환값을 포함하는 객체
- 비동기로 작동한다.
  - useQuery가 순차적으로 진행되는 것이 아니라 두가지 useQuery가 동시에 실행된다.
  - 여러 개의 query가 있다면 useQuery보다 `useQueries`를 사용하는 것이 좋다.
  - `enabled`를 사용하면 useQuery를 동기적으로 사용할 수 있다.

```js
import { useQuery } from "react-query";

const { data, isLoading, error } = useQuery(queryKey, queryFn, options);

if (isLoading) {
  return <span>Loading...</span>;
}

if (error) {
  return <span>Error</span>;
}
```

### queryKey

- 쿼리를 식별하는 고유 키이다.
- 이 키를 통해 캐싱, 업데이트, 무효화 등의 작업을 수행한다.
- 문자열 또는 배열로 지정할 수 있다.
- 배열의 요소 중 하나라도 변경되면 쿼리가 자동으로 업데이트된다.

  ```js
  // 문자열
  useQuery(('todos'), ...)

  // 배열
  useQuery(['todos', '1'], ...)
  ```

### queryFn

- 데이터를 비동기적으로 불러오는 함수이다.
- 직접 promise를 반환해야하고, 이 promise의 상태에 따라 useQuery가 반응한다.
- fetch, axios 등을 사용해서 api 호출을 실행할 수 있다.

### options

useQuery의 동작을 좀 더 세밀하게 조정할 수 있는 선택적 매개변수이다.
몇가지 주요 옵션으로는 아래와 같은 것들이 있다.

**enabled** <br/>

- 쿼리가 자동으로 실행되지 않게 막는 옵션 (동기적으로 실행하도록 함)
- boolean (default: true)

```js
const { data } = useQuery(["todos", id], queryFn, {
  enabled: !!id,
  // id가 존재할 때만 쿼리 요청을 한다.
});
```

**staleTime**

- 데이터가 fresh 상태로 유지되는 시간을 지정한다.
- number (default: 0)
- fresh 상태에서는 다시 mount 되어도 fetch가 실행되지 않는다.

**cacheTime**

- inactive인 캐시 데이터가 메모리에 남아있는 시간을 지정한다.
- number (default: 0)

**onSuccess**

- 쿼리 성공 시 실행되는 함수

**onError**

- 쿼리 실패 시 실행되는 함수

## useMutation

- 데이터를 `post`, `update`와 같이 수정 작업을 할 때 사용하는 Hook이다.
- <br/>

**참고자료**
