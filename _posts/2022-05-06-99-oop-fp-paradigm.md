---
layout: post
title: "프로그래밍의 패러다임 OOP vs FP"
author: "Nostrss"
comments: true
tags: oop fp
excerpt_separator:
sticky:
hidden:
---




## 프로그래밍 패러다임


프로그래밍 패러다임은 프로그래머에게 프로그래밍의 관점을 갖게 해 주고, 결정하는 역할을 한다.
프로그래밍 패러다임의 종류는 다양한데 대표적인 것은 아래와 같다.


- >명령형 프로그래밍
  - 절차적 프로그래밍: 수행되어야 할 연속적인 계산 과정을 포함하는 방식
  - 객체지향 프로그래밍: 객체들의 집합으로 프로그램의 상호작용을 표현

- >선언형 프르그래밍
  - 함수형 프로그래밍

발전 순서는 절차적 프로그래밍 > 객체지향 프로그래밍 > 함수형 프로그래밍 의 순서로 발전해왔다고 보면 된다.


## 객체 지향 프로그래밍(Object-Oriented Programming)

여러 개의 독립된 단위, 즉 "객체"들의 모임으로 파악하고자 하는 것이다. 각각의 객체는 메시지를 주고받고, 데이터를 처리할 수 있다.

객체 지향 프로그래밍은 프로그램을 유연하고 변경이 쉽게 만들기 때문에 대규모 소프트웨어 개발에 많이 사용된다. 또한 프로그래밍을 더 배우기 쉽게 하고 소프트웨어 개발과 보수를 간편하게 하며, 보다 직관적인 코드 분석을 가능하게 하는 장점이 있다. 그러나 지나친 프로그램의 객체화 경향은 실제 세계의 모습을 그대로 반영하지 못한다는 비판을 받기도 한다.

### OOP의 특징

1. 추상화

현실세계 대상을 관찰하여 핵심적인 특징(속성과 행위)을 뽑아내는 과정이다.
이때 관련있는 것들을 묶게되면 캡슐화가 되고 묶은 개념은 추상화가 되고 주체는 클래스가 된다.
'객체'는 클래스로 부터 실체화 된것으로 눈에 보이며 실체한다.
'클래스'는 추상적이기에 눈에 보이지 않고 개념적으로만 존재한다.

2. 캡슐화

속성과 행위를 관련있는 것끼리 묶는다.
여기서 중요한 것은 접근이 필요한 부분을 제외하고 구체적인 로직은 내부로 숨긴다(은닉성).구체적인 로직은 내부로 은닉하는 목적이다.

3. 상속

대상이 되는 클래스의 모든 특징을 물려받는 것, 이때 자식 클래스로 부터 부모 클래스가 대체되어도 의미가 성립되어야한다.

4. 계층형 구조


### OOP 언어 종류
- C++
- C#
- JAVA
- Objective-C
- Swift
- Dart

## 함수형 프로그래밍

자료 처리를 수학적 함수의 계산으로 취급하고 상태와 가변 데이터를 멀리하는 프로그래밍 패러다임의 하나이다. 명령형 프로그래밍에서는 상태를 바꾸는 것을 강조하는 것과는 달리, 함수형 프로그래밍은 함수의 응용을 강조한다

### 함수형 프로그래밍 특징

1. 일급객체

사용할때 다른 요소와 아무런 차별이 없는 객체 

2. 고차함수

함수는 함수를 파라미터로 전달할 수 있어야하며 함수의 반환값으로 함수를 사용할 수 있습니다.

(React의 고차컴포넌트는 컴포넌트를 이용하여 위의 조건을 만족하는 컴포넌트를 말한다)

 
3. 불변성

변하지 않는 성질을 말한다.

자바스크립트는 자유로운 언어로 데이터의 변경이 언제든 가능하나 안되는 언어들이 존재한다.

불변성을 지키기 위해서는 데이터 변경이 필요할 경우 원본을 유지한 채 복사본을 만들어 작업해야한다.

 

4. 순수함수

동일한 입력에는 항상 같은 값을 반환해야한다.

함수의 실행은 프로그램의 실행에 영향을 미치지말아야한다. 

함수 내부에서 인자값의 변경이나 프로그램의 상태를 변경하면 안된다.


5. 합성함수

새로운 함수를 만들거나 계산하기 위해서는 둘 이상의 함수를 조합하는 과정을 말한다.

함수형 프로그래밍은 작은 여러개의 함수들로 이루어져 있기에 이러한 함수들을 연쇄적으로 또는 병렬로 호출해서 더 큰 함수를 만드는 과정으로 전체 프로그래밍을 구축한다.




