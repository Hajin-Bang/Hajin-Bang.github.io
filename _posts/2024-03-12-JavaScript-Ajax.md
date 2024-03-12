---
title: "AJAX"
excerpt: "서버와 브라우저가 비동기 방식으로 데이터를 교환할 수 있는 통신 기능"

categories:
  - JavaScript
tags:
  - [AJAX, JavaScript]

permalink: /JavaScript/AJAX/

toc: true
toc_sticky: true

date: 2024-03-12
last_modified_at: 2024-03-12
---

# AJAX

## [요약]

> AJAX는 JavaScript의 라이브러리 중 하나이며, 웹 페이지가 서버와 비동기적으로 통신하여, 웹 페이지 전체를 새로 고침하지 않고도 일부 페이지 내용을 업데이트할 수 있게 하는 기술이다.

## AJAX란?

- Asynchronous JavaScript and XML
- JavaScript의 라이브러리이다.
- 웹 페이지가 서버와 비동기적으로 데이터를 교환하고, 그 결과를 웹 페이지에 동적으로 표시할 수 있도록 하는 기술이다.
- 웹 페이지의 일부만을 업데이트할 수 있어서 전체 페이지를 새로 고칠 필요가 없다.(SPA)
  > **AJAX는 여러 기술의 결합으로 이루어져 있다.**
  >
  > - **HTML, CSS**: 표현 담당
  > - **DOM**: 동적으로 화면에 내용을 표시하거나 변경하는 데 사용
  > - **JavaScript**: 클라이언트 측에서 사용자와의 상호작용을 처리하고, 서버와 비동기 통신을 실행
  > - **XMLHttpRequest**: 웹 페이지가 서버와 비동기적으로 데이터를 교환할 수 있게 해주는 역할
  > - 데이터 포맷으로는 XML이 전통적으로 사용되지만, **JSON**이 더 선호된다.

### AJAX의 장점

- 페이지 속도가 향상되고, 생산성이 증가된다.
- 사용자 경험이 향상된다.

### AJAX의 단점

- 클라이언트가 서버에 데이터를 요청하는 클라이언트 풀링 방식을 사용하므로, 서버 푸시 방식의 실시간 서비스는 만들 수 없다.
- 연속으로 데이터를 요청하면 서버 부하가 증가할 수 있다.
- 디버깅이 용이하지 않다.

### AJAX 프레임워크

- Prototype
- jQuery
- dojo

<br/>

**참고자료**

- https://daegwonkim.tistory.com/445
