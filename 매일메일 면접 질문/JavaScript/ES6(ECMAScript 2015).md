# ES6(ECMAScript 2015)

> 매일메일 FE 2025년 2월 4주차 월요일 질문

### 주요 변경사항

#### let, const 키워드 추가
- `let`: 변수 선언
- `const`: 상수 선언
- `var`와 달리 블록 스코프를 가져 코드의 안정성이 높음

#### 화살표 함수 도입
- 기존의 함수 정의 방식보다 간결하고 가독성이 좋음
- 호이스팅 적용이 안됨
- this가 존재하지 않아 선언될 시점에서 상위 스코프가 this로 바인딩 됨
```
// ES5
var x = function(x, y) {
    return x * y;
}

// ES6
const x = (x, y) => x * y;
```

#### 클래스 문법 추가
```
class Car {
    constructor(name, year) {
        this.name = name;
        this.year = year;
    }
}
```

#### 템플릿 리터럴 추가
- 템플릿 문자열은 따옴표("") 대신 백틱(``)을 사용하여 문자열을 정의

#### 스프레드(...) 연산자
- 반복 가능한 객체를 더 많은 요소로 확장시킴

#### 구조 분해 할당
- 배열 값과 객체 속성을 변수에 쉽게 할당시킴
```
// Create an Object
const person = {
    firstName: "John",
    lastName: "Doe",
    age: 50,
    eyeColor: "blue"
};

// Destructuring Assignment
let { firstName, age } = person;
```

#### Promise
- 자바스크립트 비동기 처리에 사용되는 객체
- 코드 생성과 코드 사용을 연결하는 객체
```
const myPromise = new Promise(function(myResolve, myReject) {
// "Producing Code" (May take some time)

  myResolve(); // when successful
  myReject();  // when error
});

// "Consuming Code" (Must wait for a fulfilled Promise).
myPromise.then(
  function(value) { /* code if successful */ },
  function(error) { /* code if some error */ }
);
```

출처: https://www.w3schools.com/js/js_es6.asp