---
layout: post
title: 'PropTypes VS Typescript'
author: 'Nostrss'
comments: true
tags: react proptypes Typescript
excerpt_separator:
sticky:
hidden:
---

개인적으로 공부하던 중에 React에서 Typescript와 같이 타입검사를 하는 PropTypes를 제공하는 것을 알게 되었다.

[React PropTypes 공식문서보기](https://ko.reactjs.org/docs/typechecking-with-proptypes.html)

## 예시

아래의 코드를 보면 Btn 컴포넌트가 props로 2개(text와 fontSize)의 값을 전달 받고 있다. 그리고 그 밑에 2개의 값에 대해 타입을 선언하는 것을 볼 수 있다.

```javascript
<!DOCTYPE html>
<html lang="en">
  <head>
    <title>Document</title>
  </head>
  <body>
    <div id="root"></div>
  </body>
  <script src="https://unpkg.com/react@17.0.2/umd/react.production.min.js"></script>
  <script src="https://unpkg.com/react-dom@17.0.2/umd/react-dom.production.min.js"></script>
  <script src="https://unpkg.com/prop-types@15.7.2/prop-types.js"></script>
  <script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>

  <script type="text/babel">
    const Btn = ({ text, fontSize = 20 }) => {
      return (
        <button
          style={{
            backgroundColor: 'tomato',
            color: 'white',
            padding: '10px 20px',
            border: 0,
            borderRadius: 10,
            fontSize,
          }}
        >
          {text}
        </button>
      );
    };

//  propTypes 선언

    Btn.propTypes = {
      text: PropTypes.string,
      fontSize: PropTypes.number.isRequired,
    };

    const App = () => {
      return (
        <div>
          <Btn text={'Save'} fontSize={18} />
          <Btn text={'Continue'} />
        </div>
      );
    };

    const root = document.getElementById('root');
    ReactDOM.render(<App />, root);
  </script>
</html>
```

선언부분만 타입스크립트와 비교해보면 상당히 유사한 것을 볼 수 있다.

> React PropTypes

```javascript
Btn.propTypes = {
  text: PropTypes.string,
  fontSize: PropTypes.number.isRequired,
};
```

> Typescript

```javascript
interface IHeaderStyle {
  isOpen?: boolean;
  isMenu?: string;
  isHidden?: boolean;
  currentPage?: any;
}
```

## 그럼 왜 Typescript를 쓸까?

이렇게 유사한 기능을 React에서 이미 제공하는데 Typescript는 왜 쓰는 걸까?

검색을 해서 몇가지 찾아봤는데 정리하면 아래와 같다.

> Typescript

- 컴파일 환경에서 타입을 체크한다.
- 코드를 작성할 때 잘못된 타입을 넘겨줄 경우 알려준다.

> React propTypes

- 런타임환경에서 타입을 체크한다
- 컴퍼넌트가 외부 Api로부터 데이터를 받아올때 잘못된 타입을 넘겨줄경우 실패 메세지로 디버깅에 도움을 준다.

같아 보이지만 자세히 보면 서로 다른 부분이 있다!!

### 둘을 같이 쓰면 더욱 좋은 것일까?

Typescript에서는 propTypes를 자동생성하는 기능을 제공한다고 한다. 그래서 타입을 2번 설정할 필요는 없다고 한다.
