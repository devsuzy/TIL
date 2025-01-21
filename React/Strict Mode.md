# 리액트의 Strict Mode

> 매일메일 FE 2025년 1월 3주차 월요일 질문

### StrictMode

- 개발 중에 컴포넌트에서 일반적인 버그 및 잠재적인 문제를 빠르게 감지하고 예방하기 위해 사용
- 개발자가 더욱 안전하고 효율적인 코드를 작성할 수 있도록 도와주는 도구

### 개발 중 이중 렌더링으로 발견한 버그 수정

- 리액트는 모든 컴포넌트가 순수 함수라고 가정
    - 동일한 입력(props, state, context)엔 동일한 JSX를 반환
- 이를 검증하기 위해 useState, useEffect, useMemo, useReducer 등 일부 훅이나 메서드를 두 번씩 실행
- 동일한 결과가 나오는지 확인함으로써 컴포넌트가 사이드 이펙트를 일으키지 않고 순수하게 동작하는지를 검사하기 위함

💡 **두 번 실행되는 현상은 개발 모드에서만 발생하고, 실제 프로덕션 빌드에서는 정상적으로 한 번만 실행되기 때문에 성능에 영향을 미치지 않는다.**

### 오래된 라이프사이클 메서드와 비권장 API 사용을 감지

- 더 이상 사용이 권장되지 않는 메서드들이 코드에 포함된 경우 경고를 표시
- `componentWillMount`, `componentWillReceiveProps`와 같은 클래스 컴포넌트 메서드

```
Fixing deprecation warnings enabled by Strict Mode
```