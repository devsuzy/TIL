#  Promise

> 매일메일 FE 2025년 2월 3주차 금요일 질문

### Promise란?
- 자바스크립트 비동기 처리에 사용되는 객체
- 해당 작업의 성공 또는 실패 결과를 나중에 사용할 수 있도록 하는 객체
- 비동기 작업의 완료 여부를 약속해주는 개념

### Promise 사용 용도
- 주로 서버에서 받아온 데이터를 화면에 표시할 때 사용
- 데이터를 받는 일과 화면에 표시하는 일을 비동기 처리함

### Promise의 3가지 상태
1. Pending(대기): 비동기 처리 로직이 아직 완료되지 않은 초기 상태
    1. `new Promise()`의 콜백함수로 `resolve`와 `reject`를 인자로 받는다.
    ```javascript
    new Promise(function(resolve, reject) {

    });
    ```
2. Fulfilled(이행) : 비동기 처리가 완료되어 프로미스가 결과 값을 성공적으로 반환해준 상태
    1. `resolve()`: 비동기 작업을 성공했을 때 funlfilled 상태로 전환
    2. `then`()`: 성공적으로 처리된 결과값을 받음
    ```javascript
    new Promise(function(resolve, reject) {
        resolve();
    });
    ```
3. Rejected(실패) : 비동기 처리가 실패하거나 오류가 발생한 상태
    1. `reject()`: 비동기 작업을 실패했을 때 rejected 상태로 전환
    2. `catch()`: 실패했을 때 처리된 결과값을 받음
    ```javascript
    new Promise(function(resolve, reject) {
        reject();
    });
    ```

### Promise 장점
- 코드의 가독성을 높이고 비동기 작업의 흐름을 제어하는데 유용하다.
- Promise를 순차적으로 연결할 수 있음 => Promise Chaining
- 병렬로 비동기 작업 처리도 가능함 => Promsie.all()

### Promise 단점
- 단일 체인에서는 에러 처리가 간단하나 여러 Promise가 중첩되면 에러 처리가 복잡하다.
- 콜백 지옥을 어느정도 해결하지만, 여러 Promise를 순차적으로 실행해야 할 때 then() 체인을 계속 사용하면 코드의 들여쓰기 구조가 복잡해지고 이해하기 어려워진다. => `async/await`를 통해 개선
