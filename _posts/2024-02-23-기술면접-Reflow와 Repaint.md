---
title: "Reflow와 Repaint"
excerpt: "Reflow와 Repaint가 실행되는 시점은?"

categories:
  - 기술면접
tags:
  - [HTML, 브라우저, Reflow, Repaint]

permalink: /기술면접/Reflow와-Repaint/

toc: true
toc_sticky: true

date: 2024-02-23
last_modified_at: 2024-02-23
---

# Reflow와 Repaint

## [요약] Reflow와 Repaint가 실행되는 시점은 언제인가?

> **Reflow** <br/>
> -CSS의 스타일 추가, 변경으로 DOM의 기하학적 속성이 변경될 때 <br/> -브라우저 사이즈가 변할 때
>
> **Repaint** <br/> -가시성이 변경되는 순간(opacity, background-color, visibility, outline) <br/>
> -Reflow가 실행된 순간 뒤에 실행

## Reflow

**Reflow**는 요소의 너비, 높이, 위치 등이 변경될 때 영향 받은 모든 노드의 수치를 다시 계산하여 렌더 트리를 재생성하는 작업을 말한다.
이때, "영향 받은"은 어떤 상황을 말하는걸까? 아래의 예시를 통해 알 수 있다.

그림처럼 위치한 세가지 박스가 있을 때,<br/>
![Group 1](../assets/images/posts_img/ReflowRepaint/Group%201.png) <br/>
만약 B의 너비를 변경한다면 당연히 Reflow가 발생할 것이다. 그런데 B의 너비를 변경함으로 인해, 인접한 A와 C의 위치도 변경되므로 Reflow가 발생한다.
즉, 요소 하나의 변화가 주변 요소의 위치나 크기에 영향을 주어, DOM 트리 계산 작업이 발생하고 렌더 트리가 재생성되는 것이다.

Reflow가 발생하는 상황은 아래와 같이 정리할 수 있다.

> -DOM 노드의 추가, 제거
>
> -DOM 노드의 위치 변경
>
> -DOM 노드의 크기 변경 (margin, padding, width, height, border 등)
>
> -CSS3 애니메이션과 트랜지션
>
> -폰트, 텍스트 내용 변경
>
> -이미지 크기 변경
>
> -페이지 초기 렌더링
>
> -윈도우 리사이징

## Repaint

**Repaint**는 Reflow 과정이 끝난 후 재생성된 렌더 트리를 다시 그리는 과정이다.
다만, Repaint가 발생하기 위해서 항상 Reflow가 발생해야하는 것은 아니다. 예를 들어, 레이아웃에 영향을 주지 않는 엘리먼트 개별의 변화에 대해서는 Repaint만 발생하게 될 것이다.

## Reflow, Repaint 최적화

Reflow와 Repaint는 비용이 드는 작업이다. 그럼 어떻게 해야 이를 줄일 수 있을까?

**1. DOM 접근을 최소화한다.** <br/>
documentFragment를 사용하자. documentFragment는 DOM이 적용되기 전까지는 메모리 상에만 존재하여, 한 번에 DOM을 추가해서 DOM 접근을 최소화 할 수 있다.

**2. 인라인 스타일을 사용하지 않는다.** <br/>
스타일 속성을 통해 스타일을 설정하면, 리플로우가 발생한다. 클래스를 사용하여 하나의 리플로우만 발생하도록 할 수 있다.

**3. 레이아웃을 위한 table은 피한다.** <br/>
table은 점진적으로 렌더링되지 않고, 모두 불려지고 계산된 다음에야 렌더링이 된다. 따라서 테이블 컨텐츠의 작은 변경만 있어도 테이블 너비가 다시 계산되고, 테이블 모든 노드에서 reflow가 발생한다.

**4. `display: none`을 사용한다.** <br/>
`display: none`이 적용된 요소는 Render Tree에서 제외된다. 만약 요소의 여러 스타일이 수정되어야하는 경우, 먼저 `display: none`을 설정하고 스타일을 변경한 뒤, `display: block`을 하는 방법이 있다.

<br/>

**참고자료**

- https://k0102575.github.io/articles/2020-11/reflow-repaint
- https://mong-blog.tistory.com/entry/%EB%A6%AC%ED%94%8C%EB%A1%9C%EC%9A%B0-%EB%A6%AC%ED%8E%98%EC%9D%B8%ED%8A%B8%EC%99%80-%EB%B8%8C%EB%9D%BC%EC%9A%B0%EC%A0%80-%EB%A0%8C%EB%8D%94%EB%A7%81-%EC%95%8C%EC%95%84%EB%B3%B4%EA%B8%B0
- https://ekimnida.tistory.com/45
