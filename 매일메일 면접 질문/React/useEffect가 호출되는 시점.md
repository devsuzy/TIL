#  useEffect가 호출되는 시점

> 매일메일 FE 2025년 2월 3주차 목요일 질문

### useEffect

- 외부 시스템과 컴포넌트를 동기화 하는 리액트의 훅
- 컴포넌트의 특정 시점에 자동으로 호출되는 훅
- 마운트, 업데이트, 언마운트되는 시점에 호출됨

### useEffect 수행 동작

```jsx
import { useEffect } from 'react';
import { createConnection } from './chat.js';

function ChatRoom({ roomId }) {
  const [serverUrl, setServerUrl] = useState('https://localhost:1234');

  useEffect(() => {
    const connection = createConnection(serverUrl, roomId); // 설정 코드
    connection.connect();
    return () => {
      connection.disconnect(); // 정리 코드
    };
  }, [serverUrl, roomId]); // 의존성 배열
  // ...
}
```
1. 마운트: 컴포넌트가 화면에 추가되었을 때 설정 코드 실행
2. 업데이트: 의존성 배열의 상태가 변경되면 컴포넌트가 리렌더링 될 때마다 정리 코드 -> 실행 코드 순서로 실행
    1. 정리 코드: 이전 props와 state와 함께 실행
    2. 설정 코드: 새로운 props와 state와 함께 실행
    3. 의존성 배열이 비어졌을 경우 매 렌더링마다 호출됨
3. 언마운트: 컴포넌트가 화면에서 제거되었을 때 정리 코드 실행

### 설정 코드와 정리 코드

- 버그를 발견하기 위해 개발모드에서 설정이 실행되기 전에 설정과 정리를 한 번 더 실행시킨다.
- 이는 Effect의 로직이 정확하게 수행되고 있는지를 검증한다.
- 정리 함수를 이용하여 이벤트 리스너 제거, 타이머 해제, 구독 취소 등의 작업을 수행할 수 있다.
    - 타이머 관리: `setInterval()`, `clearInterval()`
    - 이벤트 구독 관리: `window.addEventListenr()`, `window.removeEventLister()`
    - 애니메이션 관리: `animation.start()`, `animation.reset()`
- 이를 통해 useEffect를 통해 발생한 부수효과를 정리한다.