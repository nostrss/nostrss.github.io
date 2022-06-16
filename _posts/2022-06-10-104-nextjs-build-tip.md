---
layout: post
title: 'Next.js 빌드 시 알아둘 Tip'
author: 'Nostrss'
comments: true
tags: react nextjs build
excerpt_separator:
sticky:
hidden:
---

## 1. 폴더 구조 그대로 out 생성하기

- `build`를 했을 때 생성된 `out` 폴더의 내부 `폴더구조`가 로컬과는 다르게 생성되는 일이 있었다.
- 이때 아래와 같이 `next.config.js` 에 코드를 추가하면 로컬과 동일한 폴더 구조로 build가 된다.

```javascript
/** @type {import('next').NextConfig} */
const Dotenv = require('dotenv-webpack');
const nextConfig = {
  reactStrictMode: true,
  trailingSlash: true, // 폴더 구조 그대로 build를 해준다.
};

module.exports = nextConfig;
```

## 2. build시 eslint 무시하기

- build시 eslint 규칙 때문에 build 실패가 되는 경우가 있었다.
- 이때 아래와 처럼 코드를 추가 해주면 eslint 규칙은 무시하고 빌드가 된다.

```javascript
/** @type {import('next').NextConfig} */
const Dotenv = require('dotenv-webpack');
const nextConfig = {
  reactStrictMode: true,
  // eslint 규칙 무시
  eslint: {
    ignoreDuringBuilds: true,
  },
};

module.exports = nextConfig;
```
