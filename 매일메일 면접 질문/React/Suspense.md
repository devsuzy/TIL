# Suspense

> 매일메일 FE 2025년 3월 1주차 수요일 질문

### Suspense
- 자식 요소를 로드하기 전까지 대체 UI 보여줌
- 로딩 상태를 선언적으로 관리할 수 있기 때문에 코드 유지보수가 쉬워짐

### Props
- `children`: 렌더링 하려는 실제 UI
- `fallback`: 실제 UI가 로딩되기 전까지 대신 렌더링되는 대체 UI

```javascript
<Suspense fallback={<Loading />}>
  <SomeComponent />
</Suspense>
```
### 주의할 점
- Effect 또는 이벤트 핸들러 내부에서 가져오는 데이터를 감지하지 않는다.
- 각각 독립적으로 로딩 상태를 관리하기 때문에 데이터 준비 시점이 다를 수 있다.
- Promise 기반의 비동기 작업만 지원한다.