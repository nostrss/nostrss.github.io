---
layout: post
title: 'React 프로젝트 Github-Page에 배포하기'
author: 'Nostrss'
comments: true
tags: react deploy github portfolio blog
excerpt_separator:
sticky:
hidden:
---

# 깃허브에 react 정적 페이지 배포하기

> next.js를 사용하면 배포 방법이 다른 것 같다.확인이 필요함

## 1. 깃허브 레파지토리 생성하기

## 2. 로컬 PC에서 react 프로젝트 생성하기

```
npx create-react-app my-app
cd my-app // 생성된 폴더로 들어가야한다

```

### 3.깃허브와 프로젝트 연결하기

```
git remote add origin https://github.com/nostrss/react-deploy.git
```

또는 깃클론 한뒤 프로젝트를 생성

### 4. `gh-pages`설치

https://www.npmjs.com/package/gh-pages

`npm install gh-pages --save-dev`

### 5.`package.json` 세팅

```
{
  "name": "react-deploy",
  "version": "0.1.0",
  "private": true,

  // 홈페이지 주소 추가
  "homepage": "http://nostrss.github.io/react-deploy",


  "dependencies": {
    "@testing-library/jest-dom": "^5.16.4",
    "@testing-library/react": "^13.3.0",
    "@testing-library/user-event": "^13.5.0",
    "react": "^18.2.0",
    "react-dom": "^18.2.0",
    "react-scripts": "5.0.1",
    "web-vitals": "^2.1.4"
  },
  "scripts": {
    "start": "react-scripts start",
    "build": "react-scripts build",
    "test": "react-scripts test",
    "eject": "react-scripts eject",

     // `predeploy`, `deploy` 추가
    "predeploy": "npm run build",
    "deploy": "gh-pages -d build"
  },
  "eslintConfig": {
    "extends": [
      "react-app",
      "react-app/jest"
    ]
  },
  "browserslist": {
    "production": [
      ">0.2%",
      "not dead",
      "not op_mini all"
    ],
    "development": [
      "last 1 chrome version",
      "last 1 firefox version",
      "last 1 safari version"
    ]
  },
  "devDependencies": {
    "gh-pages": "^4.0.0"
  }
}
```

### 6. 실행(빌드)

```
npm run deploy
yarn deploy
```

- 자동으로 깃허브 레파지토리에 `gh-pages` 브랜치가 생성되고 `build`폴더 안의 파일이 푸쉬되어 올라간다.
- 소스코드는 푸쉬되지 않고 `build` 폴더안의 결과물만 올라간다.

### 7. github 세팅

- github 레파지토리 > setting > 사이드바 메뉴 > pages 로 이동
- Source 항목에서 Branch를 gh-pages로 선택

### 8. 완료

- 적용되는데 최소 5분 정도 걸린다.
- https://nostrss.github.io/react-deploy/에 접속 하면 페이지가 보인다

> 참고링크 : https://velog.io/@byjihye/react-github-pages
