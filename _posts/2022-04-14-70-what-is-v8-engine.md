---
layout: post
title: '[js] Chrome V8 엔진이란?'
author: 'Nostrss'
comments: true
tags: javascript
excerpt_separator:
sticky:
hidden:
---

앞서 Node.js 홈페이지에서 아래의 문구를 봤었다.

> Chrome V8 JavaScript 엔진으로 빌드된 JavaScript 런타임입니다.

그렇다면.. Chrome V8 JavaScript 엔진은 무엇일까?
홈페이지에 들어가서 하나씩 살펴보았다.

[Chrome V8 JavaScript 엔진 바로가기](https://v8.dev/)

>V8 is Google’s open source high-performance JavaScript and WebAssembly engine, written in C++. It is used in Chrome and in Node.js, among others.

V8은 구글의 오픈소스로 javascript와 웹어셈블리 엔진이라고 한다. 그리고 C++로 만들어져 있다고 한다. (C++의 악몽이..)

>V8 implements `ECMAScript` and `WebAssembly`, and runs on Windows 7 or later, macOS 10.12+, and Linux systems that use x64, IA-32, or ARM processors. Additional systems (IBM i, AIX) and processors (MIPS, ppcle64, s390x) are externally maintained, see ports. V8 can run standalone, or can be embedded into any C++ application.

영어의 압박이 있지만.. 중요한 것만 살펴보자.
- V8은 ECMAScript와 WebAssembly를 실행할 수 있다.
- 그리고 다양한 운영체제에서도 작동하며 여러 프로세서에서도 호환이 가능하다.
- 또한 V8은 독립적으로 작동하고 C++ 애플리케이션에 내장할 수 있다.

> V8 compiles and executes JavaScript source code, handles memory allocation for objects, and garbage collects objects it no longer needs. V8’s stop-the-world, generational, accurate garbage collector is one of the keys to V8’s performance.

오호, V8은 자바스크립트를 실행할때 메모리 할당을 하고 더이상 사용하지 않는 메모리를 다시 수거하는 역할도 하고 있었다. 내가 코드를 엉망진창으로 짜도 V8이 잘 돌아가도록 도와주고 있었던 것이다. (그동안 몰랐어 미안해 V8..)

조금더 자세하게 공부해보고 싶은데.. 영어의 압박이 있다. 오늘은 일단 여기까지..


