#  상황에 따른 this 바인딩

> 매일메일 FE 2025년 4월 3주차 화요일 질문

### 상황에 따라 달라지는 this
- 함수가 호출되는 방식에 따라 값이 달라짐
- this는 함수를 호출할 때 결정됨


### 1. 전역 호출
- **this = 전역 객체**
- 브라우저: this === window
- node: this === global
```js
function func() {
  console.log(this);
}
func(); // 브라우저: Window, Node.js: Global
```

### 2. 함수 내부 호출
- **this = 전역 객체**
- 호출 주체가 없음
- 독립적으로 호출할 경우엔 예외 없이 전역 객체를 의미
```js
var func = function () {
	console.log(this);
};
func(); // Window
```

### 3. 메서드 내부 호출
- **this = 호출의 주체**
- 자신을 호출한 대상 객체에 대한 동작을 수행
```js
const obj = {
  name: "Alice",
  greet: function () {
    console.log(this.name);
  },
};
obj.greet(); // "Alice"
```

### 4. 생성자 함수 내부 호출
- **this = 호출의 주체**
- 새로 생성되는 객체, 즉 인스턴스를 참조
```js
function Person(name) {
  this.name = name;
}
const person = new Person("Alice");
console.log(person.name); // "Alice"
```

### 5. 화살표 함수 내부 호출
- **this = 상위 스코프의 this를 상속**
- 자체적인 this를 가지지 않으므로, 사용 위치에 따라 this가 결정
- ES6에서는 함수 내부에서 this가 전역객체를 바라보는 문제 때문에 화살표 함수를 도입
- 화살표 함수는 this 바인딩 과정 자체가 없음
```js
var obj = {
	outer: function() {
		var innerFunc = () => {
			console.log(this); // obj
		};
		innerFunc();
	}
}

obj.outer();
```

### 6. 명시적 바인딩 - call(), apply(), bind()
- **this = 명시적으로 지정한 값**
- 자동으로 부여되는 상황별 this의 규칙을 깨고 this에 별도의 값을 저장하는 방법
```js
var func = function (a, b, c) {
  console.log(this, a, b, c);
};

func.call({ x: 1 }, 1, 2, 3); // { x: 1 } 1 2 3
```

### 7. DOM 이벤트 핸들러
- **this = 이벤트를 발생시킨 요소를 참조**
- 화살표 함수
    - **this = 상위 스코프의 this를 참조**
```js
button.addEventListener("click", function () {
  console.log(this); // button
});

// 화살표 함수
button.addEventListener("click", () => {
  console.log(this); 
});
```