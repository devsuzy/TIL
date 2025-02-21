# TanStack Query

> 매일메일 FE 2025년 1월 1주차 목요일 질문

### React Query? TanStack Query?

- React Query는 v4부터 react 뿐만 아니라 다른 프레임워크를 지원하면서 TanStack Query로 이름을 변경함

### TanStack Query

- 강력한 비동기 혹은 서버 상태 관리 도구

#### 주요 기능

- 캐싱
- 동일한 데이터에 대한 중복 요청을 단일 요청으로 통합
- 백그라운드에서 오래된 데이터 업데이트
- 데이터가 얼마나 오래되었는지 알 수 있음
- 데이터 업데이트를 가능한 빠르게 반영
- 페이지네이션 및 데이터 지연 로드와 같은 성능 최적화
- 서버 상태의 메모리 및 가비지 수집 관리
- 구조 공유를 사용하여 쿼리 결과를 메모화

#### 기본 설정

- Query Client
  - 캐시와 상호작용 가능
  - `defaultOptions` 설정 시 모든 `query`와 `mutation`에 기본 옵션 추가
- Query Client Provider
  - `Query Client`를 어플리케이션에 연결 및 제공
  - 최상단에 감싸주고 `Query Client` 인스턴스를 `client` prop에 넣어줌

```jsx
import { QueryClient, QueryClientProvider } from "@tanstack/react-query";

const queryClient = new QueryClient({
  defaultOptions: {
    queries: {
      staleTime: Infinity
    }
  }
});

function App() {
  return <QueryClientProvider client={queryClient}>...</QueryClientProvider>
}
```

### 핵심 개념

#### Queries

- Query Key를 기반으로 Query Caching을 진행함
- 쿼리는 서버로부터 데이터를 가져오기 위해 Promise 기반의 모든 메서드와 함께 사용 가능
- Queries의 경우 Query Key를 바탕으로 캐싱을 진행하지만, Mutations는 캐싱을 진행하지 않고 서버의 사이드 이펙트를 일으킴
  - Quereis는 GET, Mutations는 POST, PATCH, DELETE에 좀 더 적합

> **options**

- QueryKey (필수)
  - 배열로 지정
- QueryFn (필수)
  - Promise를 반환하는 함수
- staleTime
  - 데이터가 fresh에서 stale상태로 변경되는데 걸리는 시간
  - 기본값: 0
  - fresh 상태: 쿼리 호출 시 추가 네트워크 요청 없이 캐시 데이터를 사용, fetch X
  - stale 상태: 해당 쿼리 호출 시 새로운 요청을 보내 데이터를 갱신, fetch O
  - **데이터가 얼마나 오래 신선한 상태로 유지되는지를 정하는 시간**
- gcTime
  - 데이터를 사용하지 않거나 inactive 상태일 떄 캐싱된 상태로 남아있는 시간
  - 기본값: 5분
  - 설정한 시간이 지나면 가비지 컬렉션의 대상이 됨됨
  - **해당 쿼리를 사용하는 곳이 없게 된 이후에도 캐시 데이터를 얼마 동안 유지할지를 정하는 시간**

```javascript
const result = useQuery({
  queryKey: ["todos"],
  queryFn: fetchTodoList,
  staleTime: 1 * 60 * 1000,
  gcTime: 5 * 60 * 1000
})
```

> **return**

- data
  - 쿼리 요청이 성공한 경우 쿼리 함수가 리턴한 Promise에서 resolved 된 데이터
- error
  - 쿼리 함수에 오류가 발생한 경우 쿼리에 대한 오류 객체
- isPending `(status === 'pending')`
  - 캐싱된 데이터가 없고, 쿼리 시도가 아직 완료되지 않은 상태
- isLoading `isPending && isFetching`
  - 캐싱된 데이터가 없을 때 로딩 여부에 따라 true/false를 반환
- isFetching
  - 캐싱된 데이터가 있더라도 쿼리가 실행되면 로딩 여부에 따라 true/false를 반환
- isPaused
  - 네트워크가 끊어진 경우 네트워크를 다시 연결하기 전까지 쿼리 실행을 멈추고 paused상태가 됨
  - 예외 처리에 유용함함

```javascript
function Todos() {
  const { data, error, isPending, isError, isLoading, isFetching, isPaused } = useQuery({
    queryKey: ["todos"],
    queryFn: fetchTodoList,
  });

  if (isPending) {
    return <span>Loading...</span>
  }

  if (isError) {
    return <span>Error: {error.message}</span>
  }

  return {
    <ul>
      {data.map((todo) => {
        <li key={todo.id}>{todo.title}</li>
      })}
    </ul>
  }
}
```
