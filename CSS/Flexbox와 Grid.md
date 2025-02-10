#  Flexbox와 Grid

> 매일메일 FE 2025년 2월 2주차 월요일 질문

### Flex
- 한 뱡향 레이아웃 시스템 (1차원)
- 주로 행이나 열 중 하나의 방향으로 정렬
- 콘텐츠 중심으로 페이지 내 콘텐츠 추가 및 삭제에 유연하게 대처
- 버튼, 내비게이션 등 한 줄 콘텐츠 구성에 적합
- 컨텐츠 크기나 위치에 맞춰 자동으로 정렬
- 주 축 방향으로 요소를 배치하고 여백을 조절 

```
<div class="container">
	<div class="item">A</div>
	<div class="item">B</div>
	<div class="item">C</div>
</div>

.container {
	display: flex;
    flex-direction: row; // 가로, 기본값
    flex-direction: column; // 세로
    flex-wrap: nowrap; // 줄바꿈 하지 않음, 기본값
    flex-wrap: wrap; // 줄바꿈
    justify-content: flex-start; // 아이템을 시작점으로 정렬, 기본값
    align-items: stretch; // 아이템을 수직축 방향으로 끝까지 늘어남, 기본값
}

.item {
    flex-basis: auto; // 기본 점유 크기 설정, 기본값
    word-wrap: break-word; // 지정한 크기에서 컨텐츠가 넘칠 시 줄바꿈함
    flex-grow: 0; // 지정된 숫자 비율로 여백을 가져감, 기본값
    flex-shrink: 1; // 지정된 숫자 비율로 아이템 크기를 줄임, 기본값
    flex: 1 1 0; // flex-grow, flex-shrink, flex-basis
}
```
출처: https://studiomeal.com/archives/197

### Grid
- 두 방향(가로-세로) 레이아웃 시스템 (2차원)
- 행과 열을 모두 사용하여 요소를 배치
- 복잡한 레이아웃을 구성하거나 웹페이지의 전체적인 구조를 잡는데 적합
- 행과 열을 사전에 정의하고 그 격자에 요소를 배치하는 방식

```
<div class="container">
	<div class="item">A</div>
	<div class="item">B</div>
	<div class="item">C</div>
	<div class="item">D</div>
	<div class="item">E</div>
	<div class="item">F</div>
	<div class="item">G</div>
	<div class="item">H</div>
	<div class="item">I</div>
</div>

.container {
	display: grid;
    grid-template-columns: 1fr 1fr 1fr; // 그리드 트랙 열의 배치
    grid-template-rows: repeat(3, 1fr); // 그리드 트랙 행의 배치
    column-gap: 20px; // 열의 간격
    row-gap: 10px; // 행의 간격
}
```
출처: https://studiomeal.com/archives/533