---
title: "접근 제어자"
excerpt: "public, private, protected"

categories:
  - TypeScript
tags:
  - [TypeScript, 접근 제어자]

permalink: /TypeScript/접근제어자/

toc: true
toc_sticky: true

date: 2024-07-15
last_modified_at: 2024-07-15
---

# 접근 제어자

- 클래스의 특정 필드나 메서드를 접근할 수 있는 범위를 설정하는 기능
- 타입스크립트에서는 아래 3개의 접근 제어자를 사용할 수 있다.
  - public: 모든 범위에서 접근 가능
  - private: 클래스 내부에서만 접근 가능
  - protected: 클래스 내부 또는 파생 클래스 내부에서만 접근 가능

## public

- **어디서든지** 이 프로퍼티에 접근할 수 있음을 의미
- 필드의 접근 제어자를 지정하지 않으면 기본적으로 public 접근 제어자를 갖게 됨

```ts
class Employee {
  // 필드
  public name: string; // 안붙여도 public으로 설정됨
  public age: number;
  public position: string;

  // 생성자
  constructor(name: string, age: number, position: string) {
    this.name = name;
    this.age = age;
    this.position = position;
  }

  // 메서드
  work() {
    console.log(`${this.name} 일함`); // 클래스 내부에서 필드에 접근 가능
  }
}

const employee = new Employee("방하진", 26, "developer");

// 필드를 모두 public으로 설정했으므로 클래스 외부에서 접근이 가능하다.
employee.name = "홍길동";
employee.age = 29;
employee.position = "teacher";
```

## private

- **클래스 내부에서만** 이 필드에 접근할 수 있음을 의미
- 클래스 외부에서는 접근 불가능

```ts
class Employee {
  // 필드
  private name: string; // private 접근 제어자 설정
  public age: number;
  public position: string;

  // 생성자
  constructor(name: string, age: number, position: string) {
    this.name = name;
    this.age = age;
    this.position = position;
  }

  // 메서드
  work() {
    console.log(`${this.name} 일함`); // 클래스 내부이므로 필드에 접근 가능
  }
}

const employee = new Employee("방하진", 26, "developer");

employee.name = "홍길동"; // ❌ 오류! => private 필드이므로 클래스 외부에서는 접근이 불가능함
employee.age = 29; // public이므로 접근 가능
employee.position = "teacher";
```

## protected

- **클래스 내부와 파생 클래스에서** 접근할 수 있음을 의미
- 클래서 외부에서는 접근 불가능
- private과 public의 중간

```ts
class Employee {
  // 필드
  private name: string; // private 접근 제어자 설정
  protected age: number; // protected 접근 제어자 설정
  public position: string;

  // 생성자
  constructor(name: string, age: number, position: string) {
    this.name = name;
    this.age = age;
    this.position = position;
  }

  // 메서드
  work() {
    console.log(`${this.age}세 개발자`); // 클래스 내부이므로 필드에 접근 가능
  }
}

// 파생 클래스 선언
class ExecutiveOfficer extends Employee {
  // Employee 클래스를 확장하는 파생 클래스 ExecutiveOfficer 선언

  // 메서드
  func() {
    this.name; // ❌ 오류! => private 필드는 접근 불가능
    this.age; // 가능 => protected는 파생 클래스에서 접근 가능
  }
}

const employee = new Employee("방하진", 26, "developer");

employee.name = "홍길동"; // ❌ 오류! => private 필드이므로 클래스 외부에서는 접근이 불가능함
employee.age = 29; // ❌ 오류! => protected 필드이므로 클래스 외부에서는 접근이 불가능함
employee.position = "teacher";
```

## 필드 생략하기

<br/>

**참고자료**

- https://ts.winterlood.com/428ae2b8-7b91-4635-93fd-6f4103167c9b
