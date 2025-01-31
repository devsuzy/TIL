# CommonJS와 ES Module

> 매일메일 FE 2025년 1월 4주차 화요일 질문

### CommonJS
- Node.js 환경에서 주로 사용
- `require()`함수로 모듈을 가져오고, `module.export`를 사용하여 모듈을 내보냄
- 동기적으로 작동 => 모듈이 로드될 때까지 코드 실행 중단
- 서버 사이드 렌더링 환경에서 유리함
- 트리 셰이킹이 어려움 => 동적 로드를 지원하기 때문에 사용되지 않는 코드를 제거하기 어려움

### ES Module(ESM)
- 브라우저와 Node.js 환경에서 모두 사용
- `import`로 모듈을 가져오고, `export`로 모듈을 내보냄
- 비동기적으로 작동 => 브라우저에서 모듈을 로드할 때 페이지 로딩 속도를 저하시키지 않음
- 브라우저 환경에서 유리함
- 트리 셰이킹이 용이함 => 모듈의 의존성을 정적으로 분석할 수 있기 때문에 사용되지 않는 코드를 제거하여 번들 크기를 줄이는데 유리함

### CommonJS와 ES Module의 통합
- CommonJS와 ES Module 각각 제공하는 기능과 성능이 다르기 때문에 두 모듈 시스템을 통합하여 사용할 수 있다.
- Webpack과 같은 번들러를 사용하면, CommonJS와 ES Module을 모두 지원하는 번들을 생성할 수 있다.
- 프로젝트의 요구사항과 환경에 따라 적절한 모듈 시스템을 선택하고, 필요에 따라 두 모듈 시스템을 통합하여 사용할 수 있다.

```
module.exports = {
    entry: './src/index.js',
    output: {
        filename: 'bundle.js',
        libraryTarget: 'umd',
    },
    module: {
        rules: [
            {
                test: /\.js$/,
                exclude: /node_modules/,
                use: {
                    loader: 'babel-loader',
                },
            },
        ],
    },
};
```
