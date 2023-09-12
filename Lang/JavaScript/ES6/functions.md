# Functions

## Arrow Functions

arrow function은 코드를 더 쉽게 볼 수 있게 하는 것.

```jsx
const names = ["nico", "lynn", "flynn"];

// map function의 두번째 인자는 인덱스
const addHeart = names.map((item, index) => {
  console.log("we are on", index);
  return item + "💘";
});
```

## Implicit return

```jsx
const names = ["nico", "lynn", "flynn"];

// map function의 두번째 인자는 인덱스
const addHeart = names.map((item) => item + "💘");
```

implicit return 에서는 {}을 쓰면 안됨

## ‘this’ in Arrow Functions

```jsx
const button = document.querySelector("button");

button.addEventListener("click", function()
	console.log("I have been clicekd");
);
```

javascript 에는 this 키워드가 있음

예약어이고,

이벤트 리스너를 붙이고 거기에 function을 붙이면 우리가 클릭한 버튼을 this키워드에 넣음.

그러나 Arrow Function을 이용하면 this가 적용되지 않음.

이 경우, this에는 window가 출력됨

Arrow Function이 안에 있는지 밖에 있는지는 상관없음. Arrow Function이 this를 window object로 가지고 있는 것.

```jsx
const madang = {
  name: "Madang",
  age: 24,
  addYear: () => {
    this.age++;
  },
};

console.log(madang);
madang.addYear();
// 의도한 것 : age:25
console.log(madang);
// 실제 결과 : age:24(변함 없음)
```

반복하지만, Arrow Function이 안에 있는지 밖에 있는지는 상관없음. Arrow Function이 this를 window object로 가지고 있는 것.

this를 쓰려면 아래와 같이 수정

```jsx
const madang = {
  name: "Madang",
  age: 24,
  addYear() {
    this.age++;
  },
};
```

## Array Functions의 실제 활용

### Array.find()

find안에는 조건을 넣고 return 해야함

조건을 만족하는 첫번째 요소를 반환

[Array.prototype.find() - JavaScript | MDN](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/find)

### Array.filter()

주어진 함수의 테스트를 통과하는 모든 요소를 모아 새로운 배열로 반환함

[Array.prototype.filter() - JavaScript | MDN](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/filter)

### Array.forEach()

하나의 array를 반환함(함수 조건문 등으로 split같은 것을 쓸 수 없음)

[Array.prototype.forEach() - JavaScript | MDN](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach)

### map() vs forEach()

### map()

## Default Values
