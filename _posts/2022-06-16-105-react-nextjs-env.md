---
layout: post
title: 'React + Next.js .env 파일 설정하기'
author: 'Nostrss'
comments: true
tags: react nextjs build
excerpt_separator:
sticky:
hidden:
---

`git public` 레파지토리에 구글 API Key 처럼 `공개하면 안되는 정보`가 생겼다.
`.gitignore` 로 처리를 해야하나 고민하다가 .env 파일로 할 수 있다고 해서 해봤는데, 조금 헤맸던 부분이 있어서 기록 기록..

## 1. dotenv-webpack 라이브러리 설치

- 라이브러리 바로가기 : https://www.npmjs.com/package/dotenv-webpack

```javascript
npm install dotenv-webpack
// 또는 yarn add dotenv-webpack
```

## 2. .env 파일 생성

- 루트 폴더에 .env 파일을 생성한다
- 파일에는 아래와 같이 작성해준다.
- `react`에서는 꼭 변수명이 `REACT_APP`으로 시작되야 불러올수가 있다고 한다.

```javascript
REACT_APP_변수명 = 숨길 정보
// ex)  REACT_APP_GOOGLE_API_KEY=123456789abcdefg
```

## 3. next.config.js파일에서 Dotenv 플러그인을 webpack과 연결

```javascript
/** @type {import('next').NextConfig} */

const Dotenv = require('dotenv-webpack'); // 작성 1

const nextConfig = {
  reactStrictMode: true,
  webpack: (config) => {
    // 작성 2
    // 기존의 웹팩 플러그인에 새로운 Dotenv플러그인을 연결시켜준다.
    // silent는 옵션은 .env파일을 찾지 못했을 때 에러를 일으키지 않도록 설정해주는 옵션이다.
    config.plugins.push(new Dotenv({ silent: true }));
    return config;
  },
};

module.exports = nextConfig;
```

## 4. 필요한 곳에서 불러오기

- 위와 같이 설정을 다 하면 process.env.변수명(.env 파일에 작성한 이름)을 입력하면 값을 불러올 수 있다

```javascript
// 예시
 googleApiKey={process.env.REACT_APP_GOOGLE_API_KEY}
```

## 5. .gitignore에 .env 파일 추가

- 이걸 하지 않으면.. .env 파일을 생성한 의미가 없어진다..

```
# api key
.env
```

> PS : 배포 시 이슈 발생

나의 경우 배포 시 `서버`에서 소스코드를 `git pull` 한 뒤에 `build` 하여 `배포`를 하고 있었다.

그런데 `.env` 파일이 git에 올라가지 않았기 때문에 git pull을 해봤자 빌드를 해도 정상적으로 작동하지 않았다.

(.env 파일이 git에 올라가지 않게 되어 있으니깐.. 그렇다고 `gitignore`에서 제외 할 수도 없다..)

즉, 서버에 `.env`파일을 따로 업로드하고 `build`를 해줘야 하는 상황이 발생했다.

방법을 찾다가 그냥 서버에서 직접 `.env` 파일을 생성한 뒤에 빌드를 해서 처리를 했다.

> 터미널에서 .env파일 생성하는 법

```
// 파일 생성
echo  REACT_APP_GOOGLE_API_KEY=123456789abcdefg > .env

// 파일 내용 보기
cat .env
```
