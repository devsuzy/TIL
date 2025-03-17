#  Streaming SSR

> 매일메일 FE 2025년 3월 3주차 월요일 질문

### Streaming SSR란?
- 서버에서 렌더링된 HTML을 한 번에 완성해서 보내는 방식이 아니라, 준비된 부분부터 점진적으로 스트리밍해서 클라이언트에 전달하는 기술
- 서버가 데이터를 준비하는 즉시 HTML 조각을 스트림 형태로 보내고, 클라이언트는 이를 실시간으로 렌더링

```javascript
import { renderToPipeableStream } from 'react-dom/server';

const { pipe } = renderToPipeableStream(<App />, {
  bootstrapScripts: ['/main.js'],
  onShellReady() {
    response.setHeader('content-type', 'text/html');
    pipe(response);
  }
});
```

### Streaming SSR의 장점
- 초기 로딩 시간 단축 -> TTFB(Time to First Byte) 개선
- 사용자가 중요한 콘텐츠를 먼저 확인 가능 -> 사용자 경험 향상
- 기존 SSR의 한계 극복 -> 더욱 빠르고 효율적인 웹 페이지 렌더링 가능
