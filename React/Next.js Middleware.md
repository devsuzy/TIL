# Next.js Middleware

> 매일메일 FE 2025년 7월 4주차 목요일 질문

### Middleware
- 요청이 완료되기 전에 코드를 실행할 수 있음
- 서버 사이드에서 실행되며, 요청이 라우트 핸들러나 페이지에 도달하기 전에 동작
- 들어오는 요청에 따라 응답을 재작성, 리다이렉션, 응답 헤더 수정 또는 직접 응답 등을 수행 가능

### Use Cases
- 인증 및 권한 부여
    - 사용자 신원을 확인하고 특정 페이지나 API 라우트에 접근하기 전 세션 쿠키를 확인함
- 서버 측 리다이렉션
    - 특정 조건에 따라 서버 수준에서 사용자를 리다이렉션함

### 주의할 점
- Middleware는 직접적인 데이터 가져오기나 조작을 위해 설계되지 않아, 해당 로직은 서버 측 유틸리티 내에서 수행한다.
- Middleware는 가볍고 빠르게 응답해야 하며, 무거운 계산 작업이나 장기 실행 프로세스는 적절하지 않다.
- Middleware에서 광범위한 세션관리나 직접적인 데이터베이스 작업을 수행하는 것은 권장되지 않는다.

### 사용 예시
- 프로젝트 루트 또는 `src` 안에 `middleware.ts`라는 파일명으로 Middleware를 정의한다.

```ts
import { NextResponse } from 'next/server'
import type { NextRequest } from 'next/server'

export function middleware(request: NextResponse) {
    return NextResponse.redirect(new URL("/home", request.url))
}

export const config = {
    matcher: "/about/:path*"
}
```

### matcher
- `matcher`를 통해 특정 경로에서만 Middleware를 실행할 수 있도록 필터링한다.
- `matcher`은 전체 정규식을 허용하므로, 부정형 전방 탐색이나 문자 매칭과 같은 정규식 매칭이 지원된다.
```ts
export const config = {
  matcher: [
    /*
     * 다음으로 시작하는 경로를 제외한 모든 요청 경로를 매칭합니다:
     * - api (API 라우트)
     * - _next/static (정적 파일)
     * - _next/image (이미지 최적화 파일)
     * - favicon.ico (파비콘 파일)
     */
    '/((?!api|_next/static|_next/image|favicon.ico).*)',
  ],
}
```

### NextResponse
- `NextResponse` API를 통해 다음 작업을 수행할 수 있다.
    - 들어오는 요청을 다른 URL로 `redirect`
    - 주어진 URL을 표시하여 응답을 `rewrite`
    - API Routes, `getServerSideProps` 및 `rewrite` 대상에 대해 요청 헤더 설정
    - 응답 쿠키 설정
    - 응답 헤더 설정
```ts
export function middleware(request: NextRequest) {
  // 요청을 확인하기 위해 인증 함수를 호출합니다
  if (!isAuthenticated(request)) {
    // 오류 메시지를 나타내는 JSON으로 응답합니다
    return Response.json(
      { success: false, message: 'authentication failed' },
      { status: 401 },
    )
  }
}
```

### Using Cookies
- `NextRequest`와 `NextResponse`를 통해 쿠키에 쉽게 접근하고 조작할 수 있다.
    - `Request`: Cookie 헤더에 저장
    - `Response`: Set-Cookie 헤더에 저장
```ts
export function middleware(request: NextRequest) {
  // 들어오는 요청에 "Cookie:nextjs=fast" 헤더가 있다고 가정합니다
  // `RequestCookies` API를 사용하여 요청에서 쿠키를 가져옵니다
  let cookie = request.cookies.get('nextjs')
  console.log(cookie) // => { name: 'nextjs', value: 'fast', Path: '/' }
  const allCookies = request.cookies.getAll()
  console.log(allCookies) // => [{ name: 'nextjs', value: 'fast' }]
 
  request.cookies.has('nextjs') // => true
  request.cookies.delete('nextjs')
  request.cookies.has('nextjs') // => false
 
  // `ResponseCookies` API를 사용하여 응답에 쿠키를 설정합니다
  const response = NextResponse.next()
  response.cookies.set('vercel', 'fast')
  response.cookies.set({
    name: 'vercel',
    value: 'fast',
    path: '/',
  })
  cookie = response.cookies.get('vercel')
  console.log(cookie) // => { name: 'vercel', value: 'fast', Path: '/' }
  // 나가는 응답에는 `Set-Cookie:vercel=fast;path=/` 헤더가 포함됩니다.
 
  return response
}
```

### Setting Headers
- `NextResponse` API를 통해 요청 및 응답 헤더를 설정할 수 있다.
```ts
export function middleware(request: NextRequest) {
  // 요청 헤더를 복제하고 새로운 헤더 `x-hello-from-middleware1`을 설정합니다
  const requestHeaders = new Headers(request.headers)
  requestHeaders.set('x-hello-from-middleware1', 'hello')
 
  // NextResponse.next에서 요청 헤더를 설정할 수도 있습니다
  const response = NextResponse.next({
    request: {
      // 새로운 요청 헤더
      headers: requestHeaders,
    },
  })
 
  // 새로운 응답 헤더 `x-hello-from-middleware2`를 설정합니다
  response.headers.set('x-hello-from-middleware2', 'hello')
  return response
}
```
