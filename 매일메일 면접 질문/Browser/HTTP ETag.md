#  HTTP ETag

> 매일메일 FE 2026년 1월 3주차 목요일 질문

### Etag
- HTTP 프로토콜에서 사용되는 헤더
- 웹 리소스의 특정 버전을 식별하는 고유 식별자
    - 클라이언트가 이미 가지고 있는 리소스와 서버의 현재 버전이 동일한지 확인
    - 버전이 변경되지 않았다면, `304 Not Modified`응답을 받음
- 캐싱 효율성을 높임
- 네트워크 트래픽과 서버 부하를 줄임

### Etag 종류
- Strong ETag: 바이트 단위까지 정확하게 일치
- Weak ETag: 의미적으로 동등하면 일치

### 서버 -> 클라이언트 Response Header
- Cache-Control
    - 리소스 캐싱 정책을 직접적으로 지정하는 헤더
    - 캐시 가능 여부, 유효기간, 재검증 요구사항 등을 설정
    - 정적 리소스: `max-age=31536000`로 1년간 캐시 사용
    - 동적 리소스: `no-cahce`로 매번 서버에 재검증을 요청
- ETag
    - 리소스 변경 여부를 확인
```
Cache-Control: max-age=31536000
ETag: "v7d3so2jb55rv"
```

### 클라이언트 -> 서버 Requesr Header
```
If-None-Match: "v7d3so2jb55rv"
```