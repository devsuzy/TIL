# Reflow, Repaint

> 매일메일 FE 2025년 1월 1주차 화요일 질문

![browserRending](https://github.com/user-attachments/assets/0f0a6f7a-ee0b-4943-aa23-da8db843634c)


## Reflow

- 브라우저가 페이지의 레이아웃을 다시 계산하는 과정
- 모든 자식 요소와 관련된 부모 요소까지 영향을 주기 때문에 비용이 많이 드는 작업
- 노드 추가 및 제거, 위치 변경, 크기 변경, 윈도우 리사이징
- 리플로우가 발생하면 리페인트까지 발생시키는 작업

#### reflow를 유발하는 속성

- 크기 관련 속성 (width, height, padding, margin 등)
- 위치 관련 속성 (position, top, left 등)
- 레이아웃 관련 속성 (display, flex 등)
- 폰트 크기 관련 속성 (font-size, font-weight 등등)

## Repaint

- 요소의 시각적인 표현에 변화가 있을 때 변화된 표현을 다시 계산하는 과정
- 레이아웃 과정에는 영향을 미치지 않음
- 요소의 모양, 색상, 배경 등 스타일만 변경되는 경우

#### repaint를 유발하는 속성

- 색상 관련 속성 (color, background-color 등)
- 테두리 관련 속성 (border-color, border-radius 등)

### 💡 Key Point!

- reflow는 레이아웃을 다시 계산하는 과정, repaint는 계산 결과를 화면에 다시 그리는 과정
- 성능에 부하가 큰 작업이기 때문에 렌더링 성능을 최적화 하기 위해선 리플로우를 최소화 해야한다.

## Reflow와 Repaint의 성능상 차이점

#### 상위 노드와 하위 노드

- reflow - 상위 노드가 리플로우 되면 자식 노드들도 리플로우가 발생함
- repaint - 상위 노드가 리페인트 되면 자식 노드들은 리플로우와 리페인트가 발생하지 않음

#### 연산 방법

- reflow - CPU로 연산
- repaint - GPU로 연산

## Reflow를 최소화 하기 위한 방법

1. DOM 업데이트를 하나로 묶어 Batch Update 하는 방법

```
// AS-IS
for (let i = 0; i < 100; i++) {
  let item = document.createElement("div");
  item.textContext = i;
  document.body.appendChild(item);
}

// TO-BE
let fragment = document.createDocumentFragment();
for (let i = 0; i < 100; i++) {
  let item = document.createElement("div");
  item.textContext = i;
  fragment.appendChild(item);
}
document.body.appendChild(fragment);
```

2. offsetHeight, offsetWidth와 같은 레이아웃에 여러 번 접근하는 속성은 변수에 저장해두고 재사용

```
let height = element.offsetHeight;
for (let i = 0; i < 100; i++) {
  if (height > 100) {
    ...
  }
}
```

3. 영향 받는 노드 최소화 하기

- position의 경우 다른 엘리먼트 레이아웃에 영향을 주지 않는 `fixed`나 `absoulte`를 사용

4. 애니메이션 최적화

- repaint만 발생시키는 `transform`과 `opacity`속성만을 사용
- `requestAnimationFrame()` 메소드 사용
  - 지연 및 블로킹 없이 일정한 간격으로 애니메이션을 수행
  - 브라우저 프레임 속도(60fps)에 맞춰 애니메이션을 실행
  - 페이지가 비활성화 일 떄 렌더링 중지

5. `will-change` 속성 사용

- `will-change`를 통해 미리 GPU에서 요소를 준비하게끔 하여 reflow와 repaint에 미치는 영향을 줄일 수 있음
- 하지만 너무 자주 사용하면 메모리 낭비 발생 우려
