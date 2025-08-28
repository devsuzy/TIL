# localStorage와 sessionStorage

> 매일메일 FE 2025년 3월 1주차 목요일 질문

### localStorage와 sessionStorage
- 브라우저에서 제공하는 클라이언트 측 저장소 API
- 데이터를 키-값 쌍 형태로 저장
- **차이점: 데이터의 지속성과 범위**

### localStorage
- 데이터를 영구적으로 저장
- 브라우저를 닫거나 장치를 재부팅해도 데이터가 유지됨
- 동일안 도메인 내의 모든 탭에서 데이터 공유 가능
- 사용자가 지우지 않는 이상 브라우저에 계속 남아있음
- 대표적인 예: 다크모드 테마, 장바구니 데이터 등 사용자의 보안에 민감하지 않은 장기 데이터 저장에 적합

### sessionStorage
- 데이터가 현재 브라우저 세션 동안만 유지됨
- 브라우저 탭이나 창을 닫으면 데이터가 삭제됨
- 같은 도메인이여도 탭간의 데이터 공유를 하지 않음
- 대표적인 예: 일회성 로그인 정보 등 일시적인 데이터 저장에 적합

### 메소드

```javascript
// localStorage
localStorage.setItem("key", "value"); // key-value로 저장
localStorage.getItem("key"); // key로 값을 조회
localStorage.removeItem("key"); // key로 값을 삭제
localStorage.clear(); // 전체 삭제

// sessionStorage
sessionStorage.setItem("key", "value"); // key-value로 저장
sessionStorage.getItem("key"); // key로 값을 조회
sessionStorage.removeItem("key"); // key로 값을 삭제
sessionStorage.clear(); // 전체 삭제
```
- 키와 값은 모두 문자열로 반환됨
- 객체는 toString 메소드가 호출된 형태로 저장됨
    - `JSON.stringify`로 변환하여 저장
    - `JSON.parse`로 변환하여 받음 
```javascript
localStorage.setItem('object', { a: 'b' });
localStorage.getItem('object'); // [object Object]

localStorage.setItem('object', JSON.stringify({ a: 'b' }));
JSON.parse(localStorage.getItem('object')); // { a: 'b' }
```

### 문제점
- localStorage와 sessionStorage 둘다 보안 관점에서는 주의가 필요함
    - localStorage에 민감한 데이터를 저장하면 영구적으로 유지되므로 보안 위험이 높음
    - sessionStorage는 세션 종료 시 데이터가 자동 삭제되지만 여전히 보안적인 문제가 남아있음
- 인증 토큰이나 사용자 비밀번호는 HTTP-Only 쿠키를 사용
    - 자바스크립트에서 접근할 수 없음