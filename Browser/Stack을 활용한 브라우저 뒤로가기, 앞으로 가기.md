# Stack을 활용한 브라우저 뒤로가기, 앞으로 가기

> 매일메일 FE 2025년 7월 4주차 월요일 질문

<img width="407" height="241" alt="다운로드" src="https://github.com/user-attachments/assets/7db5f38c-1d71-467a-bc6e-62170bd04207" />


### 브라우저의 뒤로가기/앞으로가기 기능
- backStack(뒤로가기 스택)
  - 사용자가 방분한 페이지들이 차례대로 쌓임
  - 가장 위에 있는 페이지가 현재 페이지
- forwardStack(앞으로가기 스택)
  - 뒤로가기 한 뒤 다시 앞으로 이동
  - 이전에 방문했던 페이지들을 보관

### 새로운 페이지 방문
- `backStack.push`

### 뒤로가기 버튼
- `backStack.pop`
- `forwardStack.push`

### 앞으로가기 버튼
- `forwardStack.pop`
- `backStack.push`
