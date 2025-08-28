#  HTTP 프로토콜

> 매일메일 FE 2025년 3월 3주차 화요일 질문

### HTTP
- 웹에서 데이터를 주고받는 서버-클라이언트 모델의 프로토콜
- 클라이언트 요청 -> 서버 응답 방식으로 동작
- 한 번의 요청-응답이 끝나면 연결 종료
- 모든 통신은 안전하게 이뤄지기 위해 TCP 연결을 사용

### HTTP 요청과 응답

#### 1. 브라우저가 서버에게 HTTP 요청
```
GET /index.html HTTP/1.1 
Host: example.com
User-Agent: Mozilla/5.0
Accept-Language: ko-KR
```
- `GET`: HTTP 요청 메서드
- `/index.html`: URL 경로
- `HTTP/1.1`: HTTP 프로토콜 버전 정보
- 헤더 
    - `Host: example.com`: 웹사이트 도메인 호스트
    - `User-Agent: Mozilla/5.0`: 사용자 브라우저
    - `Accept-Language: ko-KR`: 언어

#### 2. 서버가 브라우저에게 응답
```
HTTP/1.1 200 OK
Date: Sat, 09 Oct 2023 14:28:02 GMT
Server: Apache
Content-Type: text/html

<html>
...
</html>
```
- `HTTP/1.1`: HTTP 프로토콜 버전 정보
- `200`: HTTP 상태 코드
- 헤더
- 데이터

### HTTP와 HTTPS
- HTTP: 데이터를 암호화하지 않고 전송하기 때문에 제3자가 데이터를 가로채고 읽을 수 있음
- HTTPS: 보안을 강화한 안전한 버전
    - 모든 요청과 응답을 SSL 및 TLS 프로토콜에 따라 암호화
    - 카드 정보나 비밀번호와 같은 민감한 정보 보호