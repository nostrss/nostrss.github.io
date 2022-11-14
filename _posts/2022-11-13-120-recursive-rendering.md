---
layout: post
title: '[코드지갑]재귀(?)렌더링함수'
author: 'Nostrss'
comments: true
tags: react recursive
excerpt_separator:
sticky:
hidden:
---

구조는 아래와 같고 head 객체의 깊이가 일정하지 않고 1,2,3,4,5.. 이런 순서로 페이지에 뿌려줘야 하는 경우가 발생했다.

```json
{
  "head": {
    "value": "1",
    "next": {
      "value": "2",
      "next": {
        "value": "3",
        "next": {
          "value": "4",
          "next": {
            "value": "5",
            "next": null
          }
        }
      }
    }
  },
  "tail": {
    "value": "5",
    "next": null
  },
  "length": 5
}
```

그동안 배열을 map을 이용해서 뿌려주는 방법만 사용했어서 처음에 조금 난감했는데, 재귀적으로 렌더링을 시켰더니 성공!

속도가 얼마나 날지는 모르겠지만 일단 지갑에 저장!

## Container

```typescript
const renderLinkedList = (NODE: Node, length: number) => {
  if (length === 0) return false;
  const nextNode = NODE.next;

  return (
    <div>
      <div>{NODE.value}</div>
      {renderLinkedList(nextNode, length - 1)}
    </div>
  );
};
```

## Presenter

```javascript
<div>
  {linkedList.length !== 0
    ? renderLinkedList(linkedList.head, linkedList.length)
    : ''}
</div>
```
