# Yarn과 Yarn Berry

> 매일메일 FE 2025년 7월 4주차 수요일 질문

### 기존 yarn과 npm의 특징 및 문제점
- version 1.x 시리즈
- 파일 시스템을 이용하여 의존성 관리
- `node_modules`를 이용한 비효율적인 패키지 탐색
- 복잡하고 깊은 `node_modules` 디렉토리 구조
- 매우 큰 용량 차지와 많은 I/O 작업이 필요

### Yarn Berry의 등장
- version 2.x 이상을 의미
- Plug n Play(PnP) 방식
- Zero-Install 지원''

### Yarn Berry 사용 방법
```
$ npm install -g yarn
$ yarn set version berry
$ yarn install
```

### Plug n Play(PnP)
- `node_modules` 없이 `.pnp.cjs` 파일로 의존성 관리
- `.pnp.cjs`는 디스크 I/O 없이 패키지 탐색 가능
- 각 의존성은 Zip 아카이브로 관리
- 설치 속도가 매우 빠르고 디스크 공간 절약 가능

### Zero-Install
- Yarn Berry에서 의존성을 버전 관리에 포함하는 것
- 의존성 설치(yarn install)을 하지 않음
- CI/CD에서 yarn install 단계가 생략되어 빌드와 배포 시간을 크게 단축