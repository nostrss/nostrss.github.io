---
layout: post
title: '2038년이 오면..(Unix time)'
author: 'Nostrss'
comments: true
tags: unix time epoch Y2K38
excerpt_separator:
sticky:
hidden:
---

해외 openAPI를 뒤져보다가 처음 보는 형태의 응답이 오는 경우를 발견하였다.

```json
{
  "components": {
    "co": 206.95,
    "no": 0,
    "no2": 0.59,
    "o3": 55.79,
    "so2": 1.8,
    "pm2_5": 2.37,
    "pm10": 2.39,
    "nh3": 0.01
  },
  "dt": 1606266000 // 무슨 값일까?
}
```

왠지 느낌상 날짜와 시간의 약자 같은 느낌이 들었는데, 형태가 알아보기가 어려웠다.

그래서 검색을 해보니 `Unix time`이라는 시각을 나타내는 방식이라고 한다.

## Unix Time(Epoch)

`Unix time`은 `1970년 1월 1일 00:00:00 UTC`부터의 경과 시간을 초로 환산하여 정수로 나타낸 것이라고 한다.

그래서 위의 `"dt": 1606266000`를 사람이 알아볼 수 있는 형태로 변경하면 아래와 같다.

> Wed Nov 25 2020 10:00:00 GMT+0900 (한국 표준시)

왜 1970년 1월 1일이 기준인지는 잘 모르겠지만 이 때문에 생각치 못한 `버그`들이 세상에 존재했다고 한다.

날짜를 1970년 1월 1일로 바꾸면 먹통이 되는 아이폰 버그

> [I set my iOS device to January 1, 1970...](https://discussions.apple.com/docs/DOC-9481)

## Y2K38(2038 problem)

그리고 예정된 문제가 하나 더 있는데, 바로 `2038년 문제`이다.

문제의 원인은 `32비트` 시스템에서 유닉스 타임의 표현의 한계로 인해 `오버플로`가 발생하는 것이다.

그래서 2038년 1월 19일 3시 14분 07초가 지나게 되면

1970년 1월 1일 자정으로 돌아갈 수 있다는 것이다.

아직 10년이 넘게 남았는데, 과연 그날이 오면 진짜 오류가 발생할지 궁금하긴 하다.

하긴 그때는 `2038`년이 올 줄 알았을까...