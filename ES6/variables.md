# Variables

# Why we should use Let and Const

## 1. Dead Zone

### Before temporal dead zone

```jsx
//case 1
var myName = "your name";
console.log(myName); //"your name"

//case 2
console.log(myName);
var myName = "your name"; // undefined

//case 3
console.log(myName); // Uncaught ReferenceError: myName is not defined at...
```

JavaScript는 위에서부터 아래로 코드를 읽음. 따라서 존재하지 않는 변수에 접근하려고 했기 때문에 case 2 에서는 undefined가 출력이 된 것.

반면, case 2에서는 undefined라고 출력되었던 것이 case 3에서는 에러가 뜨는 이유는 case 2에서 Hoisting되었기 때문.

### Hoisting

JavaScript가 프로그램을 실행하기 전에 변수들을 어딘가로 가지고 가는 것. 무조건 위에서 아래로 진행되는 것이 아님. case 2에서 실제로 일어났던 일은 다음과 같다.

```jsx
//case 2 => Hoisting
var myName;
console.log(myName);
myName = "your name";
```

⇒ Hoisting은 프로그램이 시작되면 변수들을 가장 위로 올려주는 것을 뜻함.

그렇다면 var 말고 let을 쓰면 어떻게 될까?

```jsx
//case 4 Use let
console.log(myName);
let myName = "your name"; // Uncaught ReferenceError: myName is not defined at...
```

에러가 발생한다. Hoisting은 let을 사용한 변수를 위로 끌어올리지않는다. 따라서 case 2와 다르게 변수를 정의하지 않았다는 에러가 발생하게 되는 것이다.

### Temporal dead zone

var를 더이상 사용하지 말아야하는 이유. 변수가 스코프 내에 있으나 정의되어있지않고, 접근할 수 없는 상태를 뜻하는 단어.

## 2. Block Scope

### Scope

scope란 기본적으로 버블이다. 이 버블이 변수가 접근 가능한지 아닌지를 감지한다.

```jsx
//case 1
if (true) {
  const hello = "hi";
  let hi = "Hello";
}

console.log(hello);
console.log(hi);
//Uncaught ReferenceError: hello is not defined at...
```

왜 오류가 발생했을까? 블록 내부에서 선언된 변수를 블록 외부에서 사용하려고 했기 때문이다. 하나의 블록은 { }로 표현하며, 버블들은 외부에서만 접근할 수 있다. (\*버블 안 버블에 변수를 선언했을 경우, 가장 안쪽에 있는 버블은 바깥에 있는 버블의 변수를 참조할 수 있으나 바깥 버블은 안쪽 버블의 변수를 참조하지 못한다. 안에서 밖으로만 볼 수 있다.) 또한 const가 아니라 let으로 선언하는 경우에도 결과는 같은 에러가 발생한다. 만약 var를 사용하면 어떻게 될까.

```jsx
//case 2
if (true) {
  var hello = "hi";
}

console.log(hello); // hi
```

var는 block scope가 아닌 function scope를 가지기 때문에 case 2가 가능하다. 그러나 다음과 같은 경우에는 에러가 발생한다.

```jsx
//case 3
function a() {
  var hello = "hi";
}

console.log(hello);
//Uncaught ReferenceError: hello is not defined at...
```

이렇게 var를 사용하면 다른 function에서 변수를 접근하게 하는건 막을 수 있으나, if 구문이나 else, try/catch 구문, for 등에서는 문제가 발생하게된다. let과 const는 블록안에서 보호를 받고 있는 것이며, 다음과 같이 사용할 수 있다.

```jsx
//case 3
if (true) {
  let hello = "hi";
}
let hello = "bye";

console.log(hello); // bye

//case 4
let hello = "hi";
if (true) {
  console.log(hello);
}

console.log(hello);
//hi
//hi
```

The future of 'var'
