#  link 요소의 rel 속성 값

> 매일메일 FE 2025년 4월 3주차 월요일 질문

### 1. preconnect
- 브라우저가 특정 origin에 대한 네트워크 연결을 미리 설정하도록 지시
- DNS 조회, TLS 핸드셰이크, TCP 연결을 미리 완료하여 리소스 로드 지연을 줄임
- 브라우저가 외부 도메인 연결에 필요한 시간을 절약할 수 있어 도메인 리소스 로드를 더 빠르게 함
- 주로 외부 API나 CDN의 리소스를 가져올 때 사용
- `crossorigin`: 리소스가 교차 출처 리소스 공유(CORS)를 사용하여 가져옴
```html
<head>
    ...
    <link rel="preconnect" href="https://external-resource.com" crossorigin="anonymous">
    ...
</head>
```

### 2. preload
- 특정 리소스를 미리 가져오도록 브라우저에 지시
- 웹 폰트를 preload하면 해당 리소스가 실제로 사용되기 전에 다운로드 됨
- 웹 폰트가 늦게 로드되면 텍스트가 기본 폰트로 잠시 표시되는 FOUT 현상이 발생할 수 있는데, 이를 방지함
```html
<head>
    ...
    <link rel="preload" href="/fonts/my-font.woff2" as="font" crossorigin="anonymous">
    ...
</head>
```

### 3. prefetch
- 브라우저가 향후 필요할 가능성이 있는 리 소스를 미리 가져오도록 지시
- 현재 화면에 즉시 필요하지는 않지만 다음에 필요할 가능성이 있는 리소르를 미리 로드
- 다른 속성에 비해 우선순위가 낮음
```html
<head>
    ...
    <link rel="prefetch" href="/next-page.css" as="style">
    ...
</head>
```

=> **preconnect, preload, prefetch는 리소스 로드의 우선순위를 설정하여 로드 성능을 최적화하기 위해 사용된다.**