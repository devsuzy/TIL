#  Virtual DOM

> 매일메일 FE 2025년 4월 1주차 목요일 질문

### Virtual DOM 탄생 배경

#### 브라우저 렌더링 과정 살펴보기
1. DOM Tree 생성 - html을 파싱하고 DOM 트리 생성
2. Render Tree 생성 - CSS 파일과 인라인 스타일을 파싱하여 렌더 트리 생성
3. Layout - 노드의 위치 및 좌표 설정
4. Painting - 모든 요소들에 색을 입히는 과정
5. UI 렌더링

=> **DOM 조작의 비효율성**
- DOM을 조작할 때마다 브라우저 렌더링 과정이 반복됨
- 많은 연산을 수반하고 비용이 많이 드는 작업임
- 이는 프로그램 성능 저하 이슈까지 이루어짐

=> **CSR 방식을 사용하는 애플리케이션 증가**
- SPA 등장으로 클라이언트 사이드 렌더링 방식이 많이 사용되면서 DOM 업데이트가 많이 필요한 애플리케이션이 증가함
- 화면을 렌더링 하는 과정의 비효율성과 최적화 문제를 해결하는 것이 숙제가 됨

### Virtual DOM이란?
- 실제 DOM node tree를 복제한 자바스크립트 객체
- 실제 DOM 보다 가벼운 사본
    - class, style 속성 ⭕️
    - DOM api 메서드 ❌

### 실제 DOM과 Virtual DOM 동작 비교
||실제 DOM|Virtual DOM|
|-|------|-----------|
|1. DOM 트리 생성|UI 렌더링|DOM 트리를 가벼운 버전으로 복사|
|2. 노드 변화 발생|DOM 트리를 다시 생성|새로운 가상의 DOM 트리를 처음부터 다시 생성|
|3. 렌더링 발생|렌더링 시 많은 비용 발생|렌더링을 하지 않고, 메모리 상에서 DOM 트리를 변경|

### Virtual DOM 동작 방식
- **상태 변경**
    - 컴포넌트의 상태나 props가 변경되면 Virtual DOM이 다시 생성
- **재조정(Reconciliation)**
    - diff 알고리즘을 이용해 새로운 Virtual DOM과 이전 Virtual DOM 간의 차이를 비교 및 계산하는 과정
- **re-render**
    - 계산된 차이에 따라 실제 DOM에서 필요한 부분만 업데이트
    - 변경된 사항만을 실제 DOM 노드에 적용하여 렌더링 수행
- 버퍼링 또는 캐싱 역할
    - DOM 조작을 할 때마다 브라우저 렌더링 과정을 반복하는 것이 아님
    - 변화된 부분을 Virtual DOM에 반영 
    - 이후 변경된 부분만 모아서 실제 DOM에 적용하여 한 번만 렌더링 실행

=> **DOM 업데이트 비용 감소, 브라우저 성능 최적화 효과를 기대**

### Virtual DOM 실행 과정
1. jsx 문법으로 코드 작성
```jsx
const element = <h1 class="foo">Hello</h1>;
```
2. Babel과 같은 컴파일러로 jsx를 js로 변환함
```js
const element = React.createElement(
    "h1",
    { title: "foo" },
    "Hello"
);
```
3. `createElement` 함수에 의해 객체로 변환함
- `type`: DOM 노드의 태그이름
- `props`: jsx에 포함된 모든 속성
    - `children`: props의 하위 노드들
```jsx
const element = {
    type: "hi",
    props: {
        title: "foo",
        children: "Hello"
    }
};
```
4. `render` 함수를 호출하여 실제 DOM 요소로 생성
```jsx
const container = document.getElementId("root");
ReactDOM.render(element, container);
```

### Diffing 알고리즘의 효율화
1. 서로 다른 타입의 두 요소는 서로 다른 트리를 만들어낸다.
    - type === type 인 경우
        - 변경 전 엘리먼트의 속성과 변경 후 엘리멘트의 속성을 비교하여 동일한 내역은 유지하고 변경된 속성들만 갱신
    - type !== type 인 경우
        - 이전 트리를 삭제하고 새로운 트리를 생성
2. key prop을 통해 여러 렌더링 사이에서 어떤 자식 엘리먼트가 변경되지 않아야 할지 표시해 줄 수 있다.
    - 자식 노드가 key 값을 가지고 있으면 key 값으로 이전 트리와 변경 트리를 비교함
    - 리스트 내역의 일부가 수정됐을 때 모든 아이템 요소들을 불필요하게 갱신하지 않고, 실제 변경된 요소만 감지하여 효율적으로 갱신
    - 변경되지 않는 유일한 값 ⭕️
    - 배열의 index 값 ❌