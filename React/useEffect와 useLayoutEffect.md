#  useEffect와 useLayoutEffect

> 매일메일 FE 2025년 2월 1주차 수요일 질문

### useEffect

- 렌더링이 완료되는 시점에 비동기적으로 실행됨
- API로부터 데이터를 가져오거나 이벤트 리스너를 추가하는 작업일 때 적합
```jsx
useEffect(() => {
    fetchData().then(data => setData(data))
}, []);
```

### useLayoutEffect

- 렌더링 후 DOM이 업데이트 되기 직전에 동기적으로 실행됨
- DOM의 크기를 측정하거나 위치를 조정해야할 때 적합
```jsx
useLayoutEffect(() => {
    const height = ref.current.offsetHeight;
    setHeight(height)
}, [])
```

### 적절한 훅 선택하기
- 비동기 작업에는 `useEffect`
- DOM 조작 및 화면에 영향을 주는 작업에는 `useLayoutEffect`