---
title: "RESTful API"
excerpt: "RESTful API란?"

categories:
  - Network
tags:
  - [Network, REST, RESTful API]

permalink: /Network/RESTful-API/

toc: true
toc_sticky: true

date: 2024-03-11
last_modified_at: 2024-03-11
---

# RESTful API

## [요약] REST, RESTful API란?

> **REST**는 자원을 이름으로 구분하여 자원의 상태를 주고 받는 것을 말하고, <br/> > **RESTful API**란 REST를 기반으로 만들어진 API를 의미한다.

## REST

- HTTP URI를 통해 자원을 명시하고, HTTP Method를 통해 해당 자원에 대한 CRUD Operation을 적용하는 것을 말한다.
- 간단하게 말하면, 자원을 이름으로 구분하여 자원의 상태를 주고 받는 것을 의미한다.

> **CRUD Operation**
>
> - Create : POST(생성)
> - Read : GET(조회)
> - Update : PUT(수정)
> - Delete : DELETE(삭제)

### REST의 구성요소

- **자원(Resource), URI**
  - 해당 소프트웨어가 관리하는 모든 것(서버에 존재하는 데이터의 총칭)
  - 모든 자원은 고유의 URI를 가지며, 클라이언트는 이 URI를 지정하여 해당 자원에 대해 CRUD 명령을 수행한다.
- **행위(Verb), Method**
  - GET, POST, PUT, DELETE와 같은 메서드를 제공한다.
- **표현(Representation)**
  - 자원을 표현하기 위한 이름
  - 하나의 자원은 JSON, XML, TEXT, RSS 등 여러 형태로 나타낼 수 있다.

### REST의 특징

- Server-Client(서버-클라이언트 구조)
- Stateless(무상태)
- Cacheable(캐시 처리 가능)
- Layered System(계층화)
- Uniform Interface(인터페이스 일관성)

### REST의 장/단점

- 장점
  - 별도의 인프라 구축이 필요 없다.
  - 플랫폼에 독립적이다.
  - 서버와 클라이언트의 역할을 명확하게 분리한다.
  - 쉽게 사용 가능하다.
- 단점
  - 표준이 존재하지 않는다.
  - 사용할 수 있는 메소드가 4가지 뿐이다. (HTTP Method)

## RESTful API

- REST 기반으로 서비스 API를 구현한 것을 말한다.

### RESTful API 설계 규칙

**1. 슬래시 구분자(/)는 계층 관계를 나타내는 데 사용한다.**
`http://restapi.example.com/houses/apartments`

- URI 경로의 마지막에는 슬래시(/)를 사용하지 않는다.
  `http://example.com/posts/` (x)

**2. 하이픈(-)은 URI 가독성을 높이는 데 사용한다.**

- 불가피하게 긴 URI 경로를 사용해야 한다면 하이픈(-)을 사용해 가독성을 높인다.

**3. 밑줄(\_)은 URI에 사용하지 않는다.**

**4. 대문자 사용은 피한다.**

- URI 경로에는 소문자가 적합하다.

**5. 파일 확장자는 URI에 포함하지 않는다.**
`http://example.com/photo.jpg` (x)
`http://example.com/photo` (o)

<br/>

**참고자료**

- https://velog.io/@seokkitdo/Network-REST%EB%9E%80-REST-API%EB%9E%80-RESTful%EC%9D%B4%EB%9E%80
- https://junvelee.tistory.com/107
