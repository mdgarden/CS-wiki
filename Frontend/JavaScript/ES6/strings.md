# Strings

## 문자열 다루기 기초 : 표현식

```jsx
// bad
const sayHi = (name = "madang") => "hello" + name;

// good
const sayHi = (name = "madang") => `hello ${name}`;
```

함수는 넣을 수 없지만 이렇게 하는 방법은 있음

```jsx
const add = (a, b) => a + b;

console.log(`hello how are you ${add(6, 6)}`);

// 함수만 쓰게 되면
console.log(`hello how are you ${add}`);
// hello how are you (a, b) => a + b
```

## HTML Fragments

js에서 html 작성하기

```jsx
const wrapper = document.querySelector(".wrapper");

const **addWelcome** = () => {
  const potato = document.createElement("div");
  const h1 = document.createElement("h1");
  h1.innerText = "Hello";
  potato.append(h1);
  wrapper.append(div);
};

setTimeOut(addWelcome, 5000);
```

- Single Quotes doesn't support multiple template literal.
