# will-change

> 유튜브 1분코딩 - CSS 애니메이션 퍼포먼스 향상시키기

### will-change
- 요소에 예상되는 변화의 종류에 관한 힌트를 브라우저에 제공
- 실제 요소가 변화되기 전에 미리 브라우저는 적절하게 최적화 가능
- 성능 비용이 큰 작업이 요구되기 전에 미리 실행함으로써 페이지의 반응성을 증가시킴

#### 주의할 점
- 너무 많은 요소에 적용하면 리소스를 많이 사용하게 되기 때문에 오히려 성능 저하를 유발

```css
/* 키워드 값 */
will-change: auto;
will-change: scroll-position;
will-change: contents;
will-change: transform; /* Example of <custom-ident> */
will-change: opacity; /* Example of <custom-ident> */
will-change: left, top; /* Example of two <animateable-feature> */

/* 전역 값 */
will-change: inherit;
will-change: initial;
will-change: unset;
```