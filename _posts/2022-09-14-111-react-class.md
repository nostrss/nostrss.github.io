---
layout: post
title: 'React Class 적응하기'
author: 'Nostrss'
comments: true
tags: react class
excerpt_separator:
sticky:
hidden:
---

회사의 React 프로젝트들에서 Class로 되어 있는 부분이 많이 있다. 그러다 보니 소스 코드를 보다 보면 아예 이해가 되지 않는 것은 아니지만
그동안 익혀왔던 함수형 만큼 익숙하지 않아서 어려움이 있는 편이다. 그래서 이제부터라도 조금씩 정리를 하면서 공부를 해야 할 것 같다.

## 클래스형 (this.state와 setState)

일단 React에서 많이 쓰는 useState를 class형에서는 아래 처럼 사용한다.

```javascript
class Clock extends React.Component {
  constructor(props) {
    super(props);
    this.state = { name: 'stress' };
  }

  render() {
    return (
      <div>
        <h1>Hello, world!</h1>
        <h2>It is {this.state.name}.</h2>
      </div>
    );
  }
}
```

`this.state = {name: stress};` 이 부분이 useState에서의 변수를 선언하는 부분이라고 생각하면 된다.
그리고 이 값을 사용하려면 `this.state.name`이라고 작성하면 된다.

그리고 name을 수정하거나 갱신하려면

```javascript
this.setState({
  name: 'nostress',
});
```

이렇게 작성해 주면 된다.

처음엔 몰랐는데 자세히 보니 결국 객체를 하나 선언해 주고, 객체를 다시 재할당 하는 것이라고 생각하니 이해와 기억하기가 좀 쉬워었다.

위의 코드를 useState로 표현하면 이렇게 될 것이다.

```javascript
const [name, setName] = useState('stress');
setName('nostress');
```
