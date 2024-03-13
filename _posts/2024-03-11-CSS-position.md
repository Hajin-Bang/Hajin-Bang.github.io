---
title: "position"
excerpt: "문서 상에 요소를 배치하는 방법을 지정하는 속성"

categories:
  - CSS
tags:
  - [CSS, position]

permalink: /CSS/position/

toc: true
toc_sticky: true

date: 2024-03-11
last_modified_at: 2024-03-11
---

# position

## [요약] CSS에서 position이란?

> position은 문서 상에 요소를 배치하는 방법을 지정하는 속성이다.
>
> - `static`: 요소를 일반적인 문서 흐름에 따라 배치
> - `relative`: 요소 원래 위치를 기준으로 `top`, `right`, `bottom`, `left` 값에 따라 상대적인 위치를 지정
> - `absolute`: 요소를 일반적인 문서 흐름에서 제거하고, 가장 가까운 조상 요소에 대해 상대적으로 배치
> - `fixed`: 요소를 일반적인 문서 흐름에서 제거하고, 항상 고정된 위치에 배치
> - `sticky`: 요소가 스크롤을 계속해서 따라오도록 배치

## position

position은 HTML 요소를 원하는 위치에 배치하기 위해 사용하는 CSS 속성이다. <br/>
position의 5가지 속성을 알아보자.

### position: static

- `position` 속성의 기본값이다.
- 일반적인 문서 흐름에 따라 원래 있어야하는 위치에 배치된다.

```html
<main>
  <div>첫번째 요소</div>
  <div>두번째 요소</div>
  <div>세번째 요소</div>
</main>
```

위의 코드처럼 구성되어 있다면, 순서대로 맨 위에 첫번째 요소, 제일 아래에 세번째 요소가 나란히 배치된다.

### position: relative

- 요소를 **원래 위치를 기준**으로, 상대적(realtive)으로 배치한다.
- `top`, `bottom`, `left`, `right` 속성을 이용해서, 기준(원래 위치)에서 얼마나 떨어지게 할지를 지정할 수 있다.

### position: absolute

- `position: static`이 아닌 **첫번째 상위 요소를 기준**으로 배치한다.
  - 가장 가까운 부모를 기준으로 절대적으로 움직인다.
- 만약 상위 요소가 없다면, `<body>`요소가 배치 기준이 된다.
- 일반적으로 `absolute`를 쓸 경우, 부모에게 `position: relative`를 부여해서 기준이 되도록 한다.

### position: fixed

- 요소를 항상 고정된(fixed) 위치에 배치한다.
- 화면을 위아래로 스크롤하더라도 요소는 브라우저 화면의 특정 부분에 고정되어 움직이지 않는다.
- 배치 기준이 뷰포트(viewport) 즉, 브라우저 전체 화면이다.

### position: sticky

- 요소가 스크롤을 계속해서 따라오게 한다.
- `static` + `position`
  - 요소를 스크롤하지 않을 때는 `static`처럼 동작하다가, 스크롤할 때는 `fixed`처럼 동작한다.
  - `top`, `bottom`, `left`, `right` 속성을 이용해서, 정해진 위치에 도달하기 전까지는 `static`, 도달 이후에는 `fixed`처럼 동작한다.

<br/>

**참고자료**

- https://www.daleseo.com/css-position/
- https://deeplify.dev/front-end/markup/position-sticky
