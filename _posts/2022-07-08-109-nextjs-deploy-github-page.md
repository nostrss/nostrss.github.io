---
layout: post
title: 'React/Next.js 프로젝트 Github-Page에 배포하기'
author: 'Nostrss'
comments: true
tags: react deploy github portfolio blog
excerpt_separator:
sticky:
hidden:
---

# 깃허브 페이지에 React && Next.js 프로젝트 배포하기

## 1. `next.js` 프로젝트 생성

## 2. `package.json` 파일 작성

- `homepage` Url 추가
- build 명령어에 `export` 추가
- `deploy` 명령어 추가

1. `next build` : next 프로젝트 빌드하고 ,static html앱으로 컴파일한 out/ 폴더를 생성해 줌
2. `touch out/.nojekyll` : Github page의 jekyll 처리과정에서 \_next 이러한 파일을 특수 리소스로 간주하고 최종 사이트에 복사하지 않는데 .nojekyll 파일을 만들면 이를 막을 수 있다.
3. `git add -f out/` : git add, out폴더가 gitignore에 포함되어 있어서 강제로 add
4. `git commit -m` : 커밋메시지 작성
5. `git subtree push —prefix out origin gh-pages` : github 저장소 gh-pages브랜치에 push

```json
{
  "name": "react-nextjs-deploy",
  "version": "0.1.0",
  "private": true,
  "homepage": "http://nostrss.github.io/react-nextjs-deploy", // homepage 추가
  "scripts": {
    "dev": "next dev",
    "build": "next build && next export", // export 추가
    "start": "next start",
    "lint": "next lint",
    // deploy 추가
    "deploy": "next build && next export && touch out/.nojekyll && git add -f out/ && git commit -m 'deploy to gh-pages' && git subtree push --prefix out origin gh-pages"
  },
  "dependencies": {
    "next": "12.2.0",
    "react": "18.2.0",
    "react-dom": "18.2.0"
  },
  "devDependencies": {
    "babel-plugin-transform-define": "^2.0.1",
    "eslint": "8.19.0",
    "eslint-config-next": "12.2.0",
    "gh-pages": "^4.0.0"
  }
}
```

## 3. `next.config.js` 파일 작성

```javascript
/** @type {import('next').NextConfig} */

const debug = process.env.NODE_ENV !== 'production';
const repository = 'react-nextjs-deploy';

const nextConfig = {
  reactStrictMode: true,
  assetPrefix: !debug ? `/${repository}/` : '', // production 일때 prefix 경로
  trailingSlash: true, // 빌드 시 폴더 구조 그대로 생성하도록
};

module.exports = nextConfig;
```

## 4. `env-config.js` 파일 작성

- 배포 후 img 등의 리소스에 접근하기 위해서 하는 작업
- 아래와 같이 세팅 해두면 프로젝트 어디에서든 앞에 `process.env.BACKEND_URL`을 추가해주면 prefix 값으로 ''(로컬일때) 또는 배포된 리소스 경로를 알아서 연결할 수 있다.

```javascript
const debug = process.env.NODE_ENV !== 'production';
const repository = 'react-nextjs-deploy';

module.exports = {
  'process.env.BACKEND_URL': !debug ? `/${repository}` : '',
};
```

## 5. `.babelrc.js` 파일 작성, `babel-plugin-transform-define` 설치

- 4번의 env-config.js 파일이 제대로 작동하기 위해 필요한 파일(?)

```javascript
const env = require('./env-config');

module.exports = {
  presets: ['next/babel'],
  plugins: [['transform-define', env]],
};
```

- `babel-plugin-transform-define` 설치

  https://www.npmjs.com/package/babel-plugin-transform-define

## 6. pages > index.js 파일의 Next.js Image 태그 영역 수정

- `Next.js`의 `Image` 태그는 `Html`의 `img` 태그와는 조금 다르므로 수정(안하면 빌드 에러 날지도)
- `src`에 위에 설정한 `prefix`를 불러오기 위해 `process.env.BACKEND_URL` 추가

```html
<img src={process.env.BACKEND_URL + '/vercel.svg'} alt='Vercel Logo' width={72}
height={16} />
```

## 7. git 레파지토리 생성 및 연결하기

## 8. 배포

> yarn deploy
> 빌드 후 out폴더의 정적파일이 업로드 됨

> 참고링크 1: https://velog.io/@ricale/next.js-%EB%A1%9C-GitHub-Pages-%EB%B0%B0%ED%8F%AC%ED%95%98%EA%B8%B0

> 참고링크 2: https://hhyemi.github.io/2021/05/26/nextGit.html

> 참고링크 3 : https://taeny.dev/javascript/nextjs-with-deployment-platform

> 참고링크 4: https://boramyy.github.io/dev/front-end/nextjs/deploy-gh-pages/

> 참고링크 5 : https://wallis.dev/blog/deploying-a-next-js-app-to-github-pages
