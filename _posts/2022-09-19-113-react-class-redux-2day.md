---
layout: post
title: '[React] 게시판 만들기 2일차'
author: 'Nostrss'
comments: true
tags: react class router redux firebase firestore
excerpt_separator:
sticky:
hidden:
---

[깃허브 소스코드 보러가기](https://github.com/nostrss/react-class-redux/tree/f974f60e10f15320c739c64bc65c9b47e90d5d5c)

## Firebase 세팅

1. `firebase` 로그인 > 콘솔로 이동
2. 프로젝트 생성
3. `App`추가(web)
4. `SDK` 설치
   > npm install firebase
5. firebase 초기화 파일 생성

- 구글 애널리틱스는 필요없을것 같아 주석처리했다.

### Firebase.js

```javascript
// Import the functions you need from the SDKs you need
import { initializeApp } from 'firebase/app';
import { getFirestore } from 'firebase/firestore';
// import { getAnalytics } from 'firebase/analytics';
// TODO: Add SDKs for Firebase products that you want to use
// https://firebase.google.com/docs/web/setup#available-libraries

// Your web app's Firebase configuration
// For Firebase JS SDK v7.20.0 and later, measurementId is optional
const firebaseConfig = {
  apiKey: process.env.REACT_APP_API_KEY,
  authDomain: process.env.REACT_APP_AUTH_DOMAIN,
  projectId: process.env.REACT_APP_PROJECT_ID,
  storageBucket: process.env.REACT_APP_STORAGE_BUCKET,
  messagingSenderId: process.env.REACT_APP_MESSAGING_SENDER_ID,
  appId: process.env.REACT_APP_APP_ID,
  measurementId: process.env.REACT_APP_MEASUR_ID,
};

// Initialize Firebase
const app = initializeApp(firebaseConfig);
export const fireBaseApp = getFirestore(app);
// const analytics = getAnalytics(fireStore);
```

키값들은 `.env`파일에 작성하여 노출이 되지 않도록 처리 했다.

이렇게 해도 프론트 쪽 키값들은 소스상에서는 노출이 되는 것으로 알긴 아는데...

찝찝한 마음에 일단은 보이지는 않게 처리 했다.

그리고 `.gitignore`에도 .env 추가

일단 이렇게만 하면 firebase를 사용할 준비는 끝이 난다.

## Class형 컴포넌트로 Firebase와 통신 해보기

일단 통신이 되는지 확인을 해보기로 했다.
텍스트 정보는 `Cloud Firestore`에 저장할 예정이다.

> [Cloud Firestore란?](!https://firebase.google.com/docs/firestore?hl=ko&authuser=0)

- input으로 텍스트를 받아 firebase로 보낸다.
- firebase에서 정보를 받아서 리스트로 보여준다.

### 전체 코드

```javascript
import React from 'react';
import { fireBaseApp } from '../../src/Firebase';
import { collection, addDoc, getDocs } from 'firebase/firestore';
import { v4 as uuidv4 } from 'uuid';

class Home extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      name: 'Home',
      inputText: '',
      firebaseData: [],
    };
  }

  /**
   * 렌더링 시 firebase로 부터 글 정보를 받아오기 위한 componentDidMount
   */
  componentDidMount() {
    this.loadFirebase();
  }

  /**
   * Firebase로 부터 data를 받아올 메소드
   */

  loadFirebase = async () => {
    const querySnapshot = await getDocs(collection(fireBaseApp, 'boards'));
    const data = querySnapshot.docs.map((doc) => doc.data());
    this.setState({
      firebaseData: data,
    });
  };

  /**
   *
   * 텍스트 입력 값을 state에 저장하는 메소드
   */
  onChangeText = (event) => {
    this.setState({
      inputText: event.target.value,
    });
  };

  /**
   * 버튼 클릭 시 firebase에 입력 값을 전달하는 메소드
   *
   */

  onSubmitForm = async (event) => {
    /**
     * 클릭 시 새로고침 되어 데이터가 사라지는 현상을 막아줌
     */
    event.preventDefault();
    try {
      await addDoc(collection(fireBaseApp, 'boards'), this.state);
    } catch (e) {
      console.error('Error adding document: ', e);
    }
  };

  render() {
    return (
      <div>
        <h1>리스트</h1>
        {this.state.firebaseData.map((board) => (
          <li key={uuidv4()}>{board.inputText}</li>
        ))}

        <form onSubmit={this.onSubmitForm}>
          <input type='text' onChange={this.onChangeText} />
          <button type='submit'>확인</button>
        </form>
      </div>
    );
  }
}

export default Home;
```

구글 문서가 자세한 듯 하면서도 내가 찾는 정보가 없어서 조금 헤매긴 했다. 구글이 문서는 자세한 듯 하면서 은근 중요한 건 찾기가 어렵..다..

[Firestore 데이터 추가하기 문서](https://firebase.google.com/docs/firestore/manage-data/add-data?hl=ko&authuser=0)

[Firestore 데이터 가져오기 문서](https://firebase.google.com/docs/firestore/query-data/get-data?hl=ko&authuser=0)

휴 일단 이렇게 class 컴포넌트도 만들어 봤고, Firebase도 연결이 된 것을 확인했다.

다음에는 redux를 사용해 봐야겠다.. 조금씩 천천히 화이팅!
