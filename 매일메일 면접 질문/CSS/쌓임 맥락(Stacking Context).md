#  쌓임 맥락(Stacking Context)

> 매일메일 FE 2025년 4월 2주차 금요일 질문

### 쌓임 맥락(Stacking Context)
![img](https://github.com/user-attachments/assets/b0e34747-ef4b-432f-96c6-9161eb0ac378)
- 가상의 z축을 상정하여 HTML 요소들을 3차원으로 개념화한 것
- 각각 HTML 요소는 자신의 속성에 따른 우선순위를 사용해 3차원 공간을 차지함

=> **쌓임 맥략을 형성한다는 것은 자신만의 3차원 공간을 형성하는 것이며 그 요소들의 우선순위를 z-index가 정하게 되는 원리**

### z-index
- 위치 지정 요소, 자손 또는 하위 플렉스 아이템의 z축 순서를 지정
    - 위치 지정 요소: position 속성의 정의되어 있는 요소(relative, absolute, sticky, fixed)
- 요소의 쌓이는 순서를 제어하는 속성
    - 여러 요소들이 겹쳐져 있을 때, 요소의 우선순위를 두어 순서를 정하는 것

### 생성 조건
- position 속성이 relative 또는 absolute이고 z-index 값이 auto가 아닌 경우
- postion 속성이 fixed 또는 sticky인 경우
- display가 flex 또는 grid이고, z-index가 설정된 경우
- opacity 값이 1 미만인 경우
- transform, filter, backdrop-filter 등의 속성이 적용되는 경우

### 동작 방식
```html
<div style="position: relative; z-index: 1;">
    A 요소 (z-index: 1)
    <div style="position: absolute; z-index: 999;">
        A-1 요소 (z-index: 999)
    </div>
</div>

<div style="position: relative; z-index: 2;">
    B 요소 (z-index: 2)
</div>
```
- B요소 > A-1요소 > A요소 순으로 쌓임
- A와 B가 이미 쌓임 맥락을 형성하고 있기 때문에(같은 레벨) A-1요소의 z-index 값이 아무리 높더라도 B요소 보다 높을 수 없음

=> **각각의 쌓임 맥락은 독립적이다.**

### position과 z-index가 아닌 다른 속성값으로 컴포넌트 위치를 조정하려면?
- 가장 아래 위치할 컴포넌트에 opacity를 1보다 낮게 설정한다.

### z-index가 동작하지 않는다면?
- z-index 값이 적절히 설정 되어있는지 확인한다.
    - 너무 낮거나 auto로 설정되어 있는지 확인
- 자식요소의 z-index 값을 방해하는 요소가 없는지 확인한다.
    - 부모요소가 쌓임 맥락을 형성하고 있으면 자식요소의 z-index가 동작하지 않을 수 있다.
