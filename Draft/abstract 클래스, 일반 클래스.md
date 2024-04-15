---
tags:
  - OOP
  - 객체지향_프로그래밍
  - 클래스
---

## 일반 클래스
타입스크립트에서 가장 기본적인 클래스 유형. 이 클래스를 사용하여 인스턴스를 직접 생성할 수 있으며, 상속도 가능함. 메소드, 속성, 생성자 등이 포함될 수 있음.

```ts
class Animal {
  name: string;

  constructor(name: string) {
    this.name = name;
  }

  move(distance: number): void {
    console.log(`${this.name} moves ${distance}m.`);
  }
}

const dog = new Animal("Dog"); // 인스턴스 생성
dog.move(10);
```

## abstract 클래스(추상 클래스)
`abstract` 클래스 자체로는 인스턴스를 생성할 수 없음. 상속을 위해 다른 클래스에서 확장되어야 함. `abstract` 메소드(구현 없이 선언만 된 메소드)를 포함할 수 있으며, 이러한 메소드는 파생된 클래스에서 반드시 구현되어야 함.

```ts
abstract class Vehicle {
  abstract makeNoise(): void; // Abstract 메소드

  move(): void {
    console.log("Moving along!");
  }
}

class Car extends Vehicle {
  makeNoise(): void {
    console.log("Vroom vroom!");
  }
}
```