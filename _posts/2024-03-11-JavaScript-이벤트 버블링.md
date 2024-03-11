---
title: "이벤트 전파(Event Propagation)"
excerpt: "이벤트 전파란?"

categories:
  - JavaScript
tags:
  - [Event Propagation, JavaScript]

permalink: /JavaScript/Event Propagation/

toc: true
toc_sticky: true

date: 2024-03-11
last_modified_at: 2024-03-11
---

# Event Propagation

## [요약] 이벤트 전파(Event Propagation)에 대해서 설명하라

> JavaScript에서 **이벤트 전파**는 이벤트가 DOM 트리를 통해 어떻게 이동하는지를 설명한다. <br/>
> 이 과정에서는 주로 두 가지 메커니즘이 포함된다.
>
> 1. 이벤트 버블링: 특정 화면 요소에서 이벤트가 발생했을 때, 해당 이벤트가 상위의 화면 요소들로 전달되어가는 과정
> 2. 이벤트 캡쳐링: 이벤트가 상위 요소에서 시작하여 발생한 위치로 내려가는 과정
>
> 이벤트 전파를 제어하기 위해 `event.stopPropagation()`을 사용할 수 있다.

## 이벤트 전파

이벤트 전파(Event Propagation)는 DOM에서 이벤트가 전달되는 과정을 설명하는 개념으로, 두 가지 단계로 이루어져 있다.

### 1. 이벤트 버블링(Event Bubbling)

- 특정 화면 요소에서 이벤트가 발생했을 때, 해당 이벤트가 상위의 화면 요소들로 전달되어 가는 과정이다.
- 최상위 요소(보통 document 객체)에 도달할 때까지 계속된다.

```html
<body>
  <div class="one">
    one
    <div class="two">
      two
      <div class="three">three</div>
    </div>
  </div>
</body>
<script>
  var divs = document.querySelectorAll("div");
  divs.forEach(function (div) {
    div.addEventListener("click", logEvent);
  });
  function logEvent(event) {
    console.log(event.currentTarget.className);
  }
</script>
```

위 코드에서는 중첩된 세 개의 `div` 코드에 모두 클릭 이벤트를 등록하고, 클릭 시 logEvent()를 실행시킨다.

여기서, 사용자가 가장 안쪽의 `div`(.three)를 클릭한다고 가정해보자. <br/>
이벤트는 먼저 해당 `div`에서 발생하고, 그 후 부모 요소로 전파된다. 즉, 이벤트는 '.three' → '.two' → '.one' 순서로 버블링된다.

> **처리 순서**
>
> 1. '.three'의 이벤트 리스너가 호출되고, 'three'가 로그된다.
> 2. 이벤트가 부모 요소인 '.two'로 버블링되고, '.two'의 이벤트 리스너가 호출되며, 'two'가 로그된다.
> 3. 이벤트가 부모 요소인 '.one'으로 버블링되고, '.one'의 이벤트 리스너가 호출되며, 'one'이 로그된다.

### 2. 이벤트 캡쳐링(Event Capturing)

- 이벤트가 상위 요소에서 시작하여 발생한 위치로 내려가는 과정이다.
- 'document' 객체에서 시작하여 이벤트가 발생한 요소로 내려간다.
- 특정 이벤트를 하위 요소보다 먼저 감지하고 싶을 때 사용한다.
- `addEventListener()`에서 옵션 객체에 `capture:true`를 설정하여 구현할 수 있다.
  - 기본값은 `false`이다.

```html
<body>
  <div class="one">
    one
    <div class="two">
      two
      <div class="three">three</div>
    </div>
  </div>
</body>
<script>
  var divs = document.querySelectorAll("div");
  divs.forEach(function (div) {
    div.addEventListener("click", logEvent, {
      capture: true, // default 값은 false
    });
  });

  function logEvent(event) {
    console.log(event.currentTarget.className);
  }
</script>
```

위 코드에서는 `addEventListener` 함수에 `{capture:true}`를 세번째 인자로 전달했다.

똑같이 사용자가 가장 안쪽의 `div`(.three)를 클릭한다고 가정해보자. <br/>
이번에는 `capture:true`로 인해 이벤트 리스너가 캡쳐링 단계에서 활성화되어, 이벤트가 타깃에 도달하기 전에 실행된다.

> **처리 순서**
>
> 1. 가장 바깥쪽의 '.one'에 대한 이벤트 리스너가 먼저 실행되고, 'one'이 로그된다.
> 2. 중간의 '.two'에 대한 이벤트 리스너가 실행되고, 'two'가 로그된다.
> 3. 실제 클릭된 가장 안쪽의 '.three'에 대한 이벤트 리스너가 실행되고, 'three'가 로그된다.

### event.stopPropagation()

`stopPropagation()`은 해당 이벤트가 전파되는 것을 막는다.

- 이벤트 버블링 : 클릭한 요소의 이벤트만 발생시키고 상위 요소로 이벤트 전달 방지
- 이벤트 캡처 : 클릭한 요소의 최상위 요소의 이벤트만 동작시키고 하위 요소로 이벤트 전달 방지

### 이벤트 위임(Event Delegation)

- 한개의 부모 요소에 리스너를 설정하고, 그 자식 요소들에서 발생하는 이벤트를 해당 리스너를 통해 처리하는 기법이다.
- 이벤트 버블링 메커니즘을 활용하여, 각각의 자식 요소에 개별적으로 리스너를 추가하지 않고도 여러 요소의 이벤트를 관리할 수 있다.

**장점**

- 메모리 사용량이 줄어든다.
- 동적인 요소를 관리하기에 용이하다.

```html
<ul id="itemList">
  <li>Item 1</li>
  <li>Item 2</li>
  <li>Item 3</li>
</ul>

<script>
  document
    .getElementById("itemList")
    .addEventListener("click", function (event) {
      console.log("List was clicked");
    });
</script>
```

html에서 여러개의 리스트 아이템이 있는 경우, 각각의 아이템에 개별적으로 클릭 이벤트를 추가하는 대신 이벤트 위임을 사용할 수 있다. <br/>
위 코드를 살펴보면 `ul`요소에 클릭 이벤트 리스너를 한번만 추가하여, 사용자가 리스트에 `li`요소를 클릭할 때마다 'List was clicked'가 콘솔에 출력된다.

> **추가 설명** <br/>
> 이 코드에서는 `ul` 요소에 클릭 이벤트 리스너를 추가했다. 그래서 `li`요소 중 하나를 클릭하면, 그 클릭한 이벤트가 발생한 `li`에서부터 시작해 상위 요소로 전파된다. **(이벤트 버블링)** 이 과정에서 `ul` 요소에 도달하게 되고, 이 때 `ul` 요소에 등록된 클릭 이벤트 리스너가 실행된다.

<br/>

**참고자료**

- https://velog.io/@klloo/JavaScript-%EC%9D%B4%EB%B2%A4%ED%8A%B8-%EC%A0%84%ED%8C%8C
