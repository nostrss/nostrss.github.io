---
layout: post
title: '나의 권한은 어디까지인가? 권한분기'
author: 'Nostrss'
comments: true
tags: react javascript nextjs
excerpt_separator:
sticky:
hidden:
---

## 권한분기

우리가 자주 사용하는 네이버 까페를 살펴보면 ID 계정 별로 등급이 나누어져 있는 것을 볼 수 있다.
예를 들면 까페장, 운영진, 일반, 미승인회원 이런식으로 말이다. 

- 까페장은 까페 가입의 승인 권한과 폐쇄 등의 모든 권한을 가지고 있다.
- 미승인회원은 까페에 글을 게시하지 못한다. 

이것처럼 각 ID계정에 따라 서비스 내에서 허가된 권한이 달라지는데 이것을 권한분기라고 한다.

### 로그인에 따른 권한 분기

현재 진행중인 프로젝트에 일단 로그인에 따른 권한 분기를 적용하려고 준비중이다.

간단히 예를 들면 로그인 회원만이 이용할 수 있는 메뉴에 접근 시 얼럿으로 '로그인 이후 이용해 주십시오'와 같은 메시지와 함께 로그인 화면으로 넘겨주는 방식으로 말이다.

### HOC(Higher Order Component)

- 특정 컴포넌트를 실행하기 전에 상위 컴포넌트를 먼저 실행시켜주는 방식이다.
- JavaScript의 클로저 함수를 이용한다.
- HOC를 하나 만들어서 로그인이 필요한 컴포넌트 앞에 HOC만 붙여주면 간단하게 권한처리를 완료한다.
- 다른 컴포넌트와 함께 실행되는 고차 컴포넌트이므로 이름 앞에 with 를 붙여준다.

즉, 마이페이지와 같이 로그인 후 이용이 가능한 페이지에 접근 할 경우 먼저 로그인 여부를 판별하는 컴포넌트를 실행시키는 것이다.

> withAuth HOC 컴포넌트
```javascript
const withAuth = (Component) => (props) => {
  const router = useRouter();
  const { accessToken } = useContext(GlobalContext);

  // 토큰체크
  useEffect(() => {
    if (!accessToken) router.push("/login");
  }, []);

  if (!accessToken) return <></>;
  return <Component {...props} />;
};

export default withAuth;
```
> 회원 전용 페이지
```javascript
const UserPage = (props) => {
  return <div>회원 페이지입니다.</div>;
};

export default withAuth(UserPage);
```

위의 예시 처럼 회원 전용 페이지에 접근 시 withAuth 컴포넌트가 먼저 실행되도록 처리하면 회원전용 페이지에 미 로그인 상태의 회원이 접근 하는 것을 분기처리 할 수 있다.

또한 이렇게 별도의 컴포넌트로 만들어 두면 추후 회원전용 페이지가 많을 경우 재사용하기가 쉽고, 유지보수가 쉬워지는 장점이 있다.

