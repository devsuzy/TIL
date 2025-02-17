#  Type과 Interface의 차이점

> 매일메일 FE 2025년 2월 3주차 월요일 질문

### Interface

- 동일한 이름으로 여러번 선언이 가능하고, 이는 자동으로 병합된다.
- 주로 객체타입을 확장할 때 유리하다.
- 확장성과 재사용성이 높아진다.
```
interface Person {
  age: number;
  name: string;
}

interface Person {
  address: string;
}

const person1: Person = {
  age: 1,
  name: "abcd",
  address: "1010",
};
```

- 객체 구조를 정의하고, 주로 클래스가 특정 구조를 따르도록 강제하는데 사용된다.
- 이는 코드의 일관성을 유지하는데 도움이 된다.
```
interface User {
    name: string;
    age: number;
}

class Person implements User {
    name: string;
    age: number;

    constructor(name: string, age: number) {
        this.name = name;
        this.age = age;
    }
}
```

### Type

- 동일한 이름으로 중복 선언을 하면 에러가 발생한다.
- 튜플과 같은 복잡한 타입 표현이 가능하며, 타입 조합을 위해 인터섹션(&)과 유니온(|) 연산자를 지원한다.
- 다양한 타입을 정의할 수 있어 더 강력한 타입 시스템을 활용할 수 있게 해준다.
```
type BasicInfo = {
  name: string;
  age: number;
};

type ContactInfo = {
  email: string;
  phone: string;
};

// 인터섹션 타입 (&)을 사용해 두 타입을 결합하여 하나의 타입으로 생성
type PersonInfo = BasicInfo & ContactInfo;

const person2: PersonInfo = {
  name: "John",
  age: 30,
  email: "john@example.com",
  phone: "123-456-7890",
};
```

- 변수, 함수 반환 값, 매개변수 등의 타입을 정의하는데 사용한다.
- 코드의 가독성과 유지보수성을 높일 수 있다.
```
type User = {
    name: string;
    age: number;
};

const user: User = {
    name: 'John',
    age: 30
};
```