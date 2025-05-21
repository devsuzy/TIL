#  Cache-Control 헤더

> 매일메일 FE 2025년 5월 3주차 수요일 질문

### Cache-Control
- 클라이언트(브라우저)와 중간 서버(proxy, CDN 등)가 어떤 방식으로 캐싱할지를 지정하는 헤더
- 특정 리소스를 얼마나 오래 저장할 수 있는지를 서버가 결정하는 것
- 한번 브라우저에 캐시가 저장되면 만료될 때까지 캐시는 계속 브라우저에 남아 있게됨

### 캐싱의 장점
- 리소스를 매번 다시 다운로드하지 않고 저장된 데이터를 활용하기에 성능 향상 효과 기대
    - 리소스(Resource): 웹 브라우저가 HTTP 요청으로 가져올 수 있는 모든 종류의 파일, HTML, CSS, JS, 이미지, 비디오 파일 등
- 불필요한 네트워크 요청을 줄이고 웹 성능을 개선할 수 있는 방법 중 하나
- 사용자의 대역폭 소비를 줄이고 그에 따라 서버 부하를 낮추며 페이지 로딩 속도를 개선하는 효과 기대

### 캐시 생명주기
#### `max-age=<seconds>`
- 해당 리소스의 캐시가 유효한 시간은 `<seconds>`초
- `max-age=31536000` - 1년(31,536,000초)

#### `no-cahce`
- 캐시는 저장하지만 사용하려고 할 때마다 서버에 재검증 요청을 보냄
- `max-age`와 동일한 뜻

#### `no-store`
- 캐시 저장소에 해당 리소스를 저장하지 않음
- 캐시를 절대로 해서는 안 되는 리소스에 사용
- 가장 강력한 값

#### `public`과 `private`
- `public`: 모든 사람과 중간 서버가 캐시를 저장할 수 있음
- `private`: 가장 끝의 사용자 브라우저만 캐시를 저장할 수 있음

#### `s-maxage`
- 중간 서버에서만 적용되는 `max-age` 값을 설정
- `s-maxage=31536000, max-age=0` - CDN에는 1년간 캐시되고, 브라우저에는 매번 재검증 요청을 보냄

**=> 정적인 리소스: `Cache-Control: public, max-age=31536000, immutable`**

**=> 동적인 리소스: `Cache-Control: no-cache, must-revalidate`**

### 실무에서 사용한 예제
```ts
app.use(
  express.static(rootDir, {
    setHeaders: (res, path) => {
      if (path.match(/\.(jpg|jpeg|png|gif|svg|webp|css|js)$/i)) {
        // 이미지 파일에 대해 1일(24시간) 캐시 설정
        res.setHeader("Cache-Control", "public, max-age=86400, must-revalidate");
      }
    },
  })
);
```

