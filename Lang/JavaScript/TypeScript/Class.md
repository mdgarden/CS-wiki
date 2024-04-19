
### Class (클래스)

클래스는 객체의 설계도로, 객체의 상태(속성)와 행동(메소드)을 정의합니다. TypeScript에서 클래스는 상속, 캡슐화, 다형성과 같은 객체 지향 프로그래밍의 핵심 개념을 구현하는 데 사용됩니다.

```ts
class Animal {
  constructor(public name: string) {}

  speak() {
    console.log(`${this.name} makes a sound.`);
  }
}

let dog = new Animal("Dog");
dog.speak(); // Dog makes a sound.

```