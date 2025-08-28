#  infer

> 매일메일 FE 2025년 5월 2주차 금요일 질문

### infer 키워드
- 조건부 타입에서 특정 타입을 추론하는데 사용
- 타입을 직접 지정하는 게 아니라 타입스크립트가 해당 타입을 유추할 수 있도록 돕는 역할
- `extend`를 사용하는 조건부 타입 안에서만 활용

### 코드 예시 - 1
```ts
type ElementType<T> = T extends (infer ArrayElement)[] ? ArrayElement : T
```

### 코드 예시 - 2
```ts
type GetReturnType<T> = T extends (...args: any[]) => infer R ? R : never;
```

### 코드 설명 - 1
```ts
type ElementType<T> = T extends string[] ? string : T;
type ElementType<T> = T extends number[] ? number : T;
type ElementType<T> = T extends boolean[] ? boolean : T;
type ElementType<T> = T extends never[] ? never : T;
```
- ElementType 타입의 제네릭으로 어떤 타입이 할당될진 모르겠지만 일단 배열 타입이다.
- 문자열(string), 숫자(number), 진위값(boolean) 등 어떤 배열 타입이 들어와도 취급해줘.

### 코드 설명 - 2
```ts
type Result = ReturnTypeOf<() => boolean>; // boolean
type Result = ReturnTypeOf<() => string>; // string
```
- `() => infer R`은 반환 타입으로 어떤 타입이 올지 모른다.
- `T`가 함수 타입이라면 infer R을 통해 반환 타입을 R로 추론하고, 그렇지 않으면 `never`를 반환한다.