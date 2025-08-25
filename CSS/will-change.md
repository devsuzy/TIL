#  box-sizing

> 매일메일 FE 2025년 4월 1주차 월요일 질문

### box-sizing
- 요소의 너비와 높이를 계산하는 방법을 지정
- CSS에서 요소의 크기를 어떻게 계산할지를 결정하는 속성

### box-sizing options

#### 1. box-sizing: content-box (기본값)
- 요소의 width와 height 값이 **내용 영역**의 크기를 나타냄
- padding과 border는 크기에 포함하지않음

#### 2. box-sizing: border-box
- 요소의 width와 height 값이 **내용 영역, padding, border** 모두 포함함

```css
div {
  width: 160px;
  height: 80px;
  padding: 20px;
  border: 8px solid red;
  background: yellow;
}

.content-box {
  box-sizing: content-box;
  /* Total width: 160px + (2 * 20px) + (2 * 8px) = 216px
     Total height: 80px + (2 * 20px) + (2 * 8px) = 136px
     Content box width: 160px
     Content box height: 80px */
}

.border-box {
  box-sizing: border-box;
  /* Total width: 160px
     Total height: 80px
     Content box width: 160px - (2 * 20px) - (2 * 8px) = 104px
     Content box height: 80px - (2 * 20px) - (2 * 8px) = 24px */
}

```