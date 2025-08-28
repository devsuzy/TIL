# CORS(Cross-Origin Resource Sharing)

> 매일메일 FE 2025년 2월 4주차 금요일 질문

### 개념 정리
<img width="1408" alt="cors-url" src="https://github.com/user-attachments/assets/067f0f76-5beb-40fe-83c1-8600c9f06eb9" />

- SOP(Same-Origin Policy)
    - 동일 출처 정책
    - 다른 출처로의 리소스 요청을 제한하는 정책
- Origin(출처)
    - Protocol과 Hostname, Port 세 가지 요소를 포함
    - 출처를 구성하는 세 요소 중 하나라도 다르면 SOP 에러가 발생함
- CORS(Cross-Origin Resource Sharing) 
    - 교차 출처 리소스 공유
    - 서로 다른 출처에서 제공되는 리소스에 접근할 수 있도록 허용하는 정책

### CORS를 적용하는 방법
```
Access-Control-Allow-Origin: * | <origin>
```
- 서버 측에서 `Access-Control-Allow-Origin` 헤더를 설정
- `*`: 출처 상관 없이 모든 도메인에서 리소스 접근 가능
- `<origin>`: 특정 출처만 접근 가능
