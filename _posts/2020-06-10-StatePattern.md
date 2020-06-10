---
layout: post
title: '[Design Pattern] 스테이트 패턴'
subtitle: '스테이트 패턴의 개념을 이해하고 구현할 수 있다.'
date: 2020-06-10
author: hansol Kim
image: '/assets/article_images/designPattern/designPattern.jpg'
categories: designPattern
tags: featured
comments: true
sitemap :
  changefreq : daily
  priority : 1.0
---



## 스테이트 패턴이란?

* 상태에 따라 동일한 작업이 다른 방식으로 실행될 때 해당 상태가 작업을 수행하도록 위임하는 디자인 패턴이다.

### 상태란?

* 객체가 시스템에 존재하는 동안, 객체가 가질 수 있는 어떤 조건이나 상황을 표현.
* 즉, 어떤 액티비티를 수행하거나 특정 이벤트가 발생하기를 기다리는 것

## 형광등 만들기 예시

### 형광등 기존 설계
![형광등의 상태머신 다이어그램](https://user-images.githubusercontent.com/31653025/84247874-9f2e6d80-ab43-11ea-91f1-aad36c8ff9a7.PNG)

* 형광등의 ON, OFF의 상태를 나누어 설계

### 문제점
* 형광등에 새로운 상태가 추가될 경우 코드확장에서 문제가 발생한다.
* 상태 추가 시 메서드 내에서 상태에 따른 코드를 수정해야 한다.(**OCP원칙 위배**)
* 메서드 내에서 상태에 따른 코드 수정 시 **if/else**문이 증가하게 된다.(이는 즉 올바른 설계가 되지 못한다.)

### 해결책
* 무엇이 변화되었는지 찾아야한다.(스트래티지 패턴과 동일)
* 변화된 것을 클래스로 캡슐화해야 한다.
* 형광등의 상태가 변화되었기 때문에 이를 클래스로 캡슐화한다.

### 스테이트 패턴을 적용한 형광등 클래스 다이어그램
![스테이트 패턴으로 구현한 형광등 상태머신 다이어그램](https://user-images.githubusercontent.com/31653025/84255130-29c79a80-ab4d-11ea-982f-c64545119cb3.PNG)

* **Sleeping** 상태가 추가되었으나 State인터페이스만 참조하므로 기존코드를 수정할 필요가 없다.
* Light클래스에서 구체적인 상태가 아닌 추상화된 State인터페이스만 참조
* 현재 어떤 상태에 있는지 무관하게 코드를 작성할 수 있다.(이는 즉, if/else문이 필요가 없게된다.)
* Light클래스에서는 상태클래스에 작업을 위임하기만 하면 된다.

## 스테이트 패턴 클래스 다이어그램
![스테이트 패턴 다이어그램](https://user-images.githubusercontent.com/31653025/84248664-b3bf3580-ab44-11ea-9648-9d6fe577a071.PNG)

* State : 시스템의 모든 상태에 공통의 인터페이스를 제공한다. 따라서 이 인터페이스를 실체화한 어떤 상태 클래스도 기존 상태 클래스를 대신해 교체해서 사용할 수 있다.

* ConcreteState : Context객체가 요청한 작업을 자신의 방식으로 실제 실행한다. 대부분의 경우 다음 상태를 결정해 상태 변경을 Context 객체에 요청하는 역할도 수행한다.

* Context : State를 이용하는 역할 수행한다. Context요소를 구현한 클래스의 request메서드는 실제 행위를 실행하지 않고 해당 상태 객체에 행위 실행을 위임한다. 

## 참조
> - [JAVA 객체지향 디자인 패턴 정인상, 채흥석 저]