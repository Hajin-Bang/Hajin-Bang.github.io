---
title: "브라우저의 렌더링 원리"
excerpt: "브라우저는 어떻게 동작하는가?"

categories:
  - 면접대비
tags:
  - [HTML, 브라우저]

permalink: /면접대비/브라우저의 렌더링 원리/

toc: true
toc_sticky: true

date: 2024-02-22
last_modified_at: 2024-02-22
---

# 브라우저의 렌더링 원리

## [요약] 브라우저의 렌더링 원리

> **1. 서버로부터 응답받은 HTML, CSS 문서를 파싱하여, DOM, CSSOM을 생성한다. (Parsing)**
>
> **2. DOM, CSSOM을 결합하여 Render Tree를 생성한다. (Style)**
>
> **3. Render Tree에서 각 노드의 위치와 크기를 계산한다. (Layout)**
>
> **4. 계산된 값을 이용해 각 노드를 화면상의 실제 픽셀로 변환하고, 레이어를 만든다. (Paint)**
>
> **5. 화면에 HTML요소를 페인팅한다. (Composite)**

## 브라우저의 주요 구성 요소

**1. 사용자 인터페이스**: 주소 표시줄, 이전/다음 버튼, 북마크 메뉴 등의 요청한 페이지를 보여주는 창을 제외한 나머지 모든 부분

**2. 브라우저 엔진**: 사용자 인터페이스와 렌더링 엔진 사이의 동작을 제어

**3. 렌더링 엔진**: 요청받은 콘텐츠 표시 => 요청받은 내용을 브라우저 화면에 표시

- 게코(Gecko)엔진: 파이어폭스에서 사용하는 렌더링 엔진
- 웹킷(Webkit)엔진: 사파리에서 사용하는 렌더링 엔진
- 블링크(Blink)엔진: 크롬에서 사용하는 렌더링 엔진 (웹킷에서 블링크로)
- **기본 동작 과정:** 파싱 -> 렌더트리 구축 -> 렌더트리 배치 -> 렌더트리 그리기

**4. 통신**: HTTP 요청과 같은 네트워크 호출에 사용

**5. UI 백엔드**: 렌더링 엔진에서 생성된 렌더 트리를 브라우저에 그리는 역할

**6. 자바스크립트 해석기**: JavaScript 코드를 해석하고 실행

**7. 자료 저장소**: 자료를 저장하는 계층

## 브라우저 렌더링

### Parsing

브라우저가 코드를 이해하고 사용할 수 있는 구조로 변환하는 과정이다. **HTML** 파일을 해석하여 **DOM(Document Object Model) Tree**를 구성하고, 파싱 중 HTML에 **CSS**가 포함되어 있다면 **CSSOM(CSS Object Model) Tree** 도 함께 구성한다.

### Style

DOM Tree와 CSSOM Tree의 결합으로 Render Tree가 만들어진다. 이는 실제로 화면에 그려질 Tree이다.

### Reflow

모든 노드의 수치를 다시 계산하여 렌더 트리를 재생성하는 작업을 말한다.

### Repaint

reflow 과정이 끝난 후 Render Tree를 다시 그리는 작업을 말한다.

## 🚨 브라우저 렌더링 과정에서 JavaScript를 만난다면?

브라우저 렌더링 과정에서 JavaScript를 만나면, 렌더링 엔진은 HTML 파싱을 일시 중단한다. >그리고 JavaScript 파일을 파싱하기 위해 JavaScript 엔진에게 제어권을 넘긴다. 이후, >JavaScript 파싱과 실행이 종료되면 다시 렌더링 엔진으로 제어권을 넘겨 HTML 파싱이 중단된 >지점부터 다시 시작한다.

렌더링 과정에서 JavaScript를 만나는 상황은 아래와 같이 `link`나 `script` 태그로 외부 리소스를 로드하는 경우를 예로 들 수 있다.

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8" />
    <link rel="stylesheet" href="style.css" />
    <script src="app.js"></script>
    ...
  </head>
</html>
```

<br/>

**참고자료**

- https://d2.naver.com/helloworld/59361
- https://tecoble.techcourse.co.kr/post/2021-10-24-browser-rendering/
- https://aldrn29.tistory.com/143
