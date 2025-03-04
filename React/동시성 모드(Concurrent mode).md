# 동시성 모드(Concurrent mode)

> 매일메일 FE 2025년 3월 1주차 화요일 질문

### 동시성 모드란?

- 여러 작업을 비동기적으로 동시에 처리하면서도 중간에 더 중요한 작업이 들어오면 우선순위를 바꿔 중요한 작업을 먼저 처리하는 기능

### 주요 특징
- 렌더링 작업의 우선순위 지정
- 렌더링 중단 및 재개 가능
- 불필요한 렌더링 방지

### 사용해보기
- Concurrent Mode를 활성화
    - `createRoot()`
```javascript
import ReactDOM from 'react-dom/client';
import App from './App';

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(<App />);
```

- `useTransition`
    - 우선순위가 낮은 상태 업데이트를 표시
    - `isPending` : 현재 상태 업데이트가 진행중인지 끝나서 보여줄 준비가 되어있는지를 판단 / boolean type
    - `startTransition` : 콜백함수 안에서 우선순위를 낮춰 렌더링할 함수를 실행 / Function type
```javascript
function TabContainer() {
  const [isPending, startTransition] = useTransition();
  const [tab, setTab] = useState('about');

  function selectTab(nextTab) {
    startTransition(() => {
      setTab(nextTab); // 낮은 우선순위
    });
  }
  // ...
}
```

- `useDeferredValue`
    - 값의 업데이트를 지연시킴 / 값처럼 사용
```javascript
const [state , setState] = useState("")
const deferredValue = useDeferredValue(state)

// ...

return (
    <div>
        deferredValue.map((v)=> <li>{v}</li>) // 기존 State처럼 사용
    </div>
)
```

### 주의할 점
- 모든 컴포넌트에 동시성 모드를 무분별하게 적용하면 오히려 성능이 떨어질 수 있다.
- 필요한 부분에만 동시성 모드를 잘 활용하는 것이 중요

### 필요한 경우
- 사용자와 상호작용이 빈번하고 응답성이 중요한 경우
    - 검색 필터링, 자동 완성 같은 기능
    - 무거운 데이터나 리스트를 로딩
    - 애니메이션이 포함된 화면 전환이나 중요도가 높은 사용자 입력 작업