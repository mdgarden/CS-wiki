# 지금 바로 써먹을 수 있는 JavaScript 클린코드 팁

자바스크립트 문법 자체보다는 문법을 어떻게 활용하는지에 대해 작성해보았습니다.

## if-else문 관련

개인적인 견해) if문과 관련된 코드가 깔끔하게 써지지 않을 때는, 대부분 높은 확률로 로직이 제대로 정비되어있지 않은 경우가 많았습니다. 하나의 함수가 한가지의 일만 수행하고 있는지, 매개변수가 지나치게 많지는 않은지, 조건문이 타당한지 여러번 재검토 해보세요.

### 조건문이 길어질 때

조건문 자체를 정수에 넣어 보기 쉽게합니다.

```jsx
// bad
if (a === "dog" || a === "cat" || a === "fish" ) {
	doSomething()
}


// better
const isPet = (a === "dog" || a === "cat" || a === "fish")
                      
if (isPet){
   doSomething()
}

```


### if문 자체가 너무 많을 때, 이중, 삼중 if문을 쓰고 있을 때

불필요한 if문을 사용하고 있지 않은지 로직을 재점검합니다.
switch문처럼 if문을 사용하고 있지 않은지 확인합니다.
간단한 실행문이라면 논리연산자를 활용합니다.

```jsx
// bad
function canDrink(person) {

if (person?.age != null) {

if (person.age < 18) {

console.log("飲めません！");

} else if (person.age < 21) {

console.log("アメリカでは飲めません!");

} else {

console.log("かんぱーい！🍻");

}

} else {

console.log("人ではありません🙅‍♀️")

}

}

  
// good
function canDrinkBetter(age) {

if (age < 18) return "飲めません！"

if (age < 21) return "アメリカでは飲めません！"

return "かんぱーい！🍻"

}

  

const result = canDrinkBetter(person.age)

console.log(result)
```

```jsx
if (foo) {
  doSomething();
}

// like this
if (foo) doSomethig();

// or like this
foo && doSomething();
```

if문 자체가 불필요한 경우가 있을 수 있음

### else문이 많아질 때

불필요한 if문을 사용하고 있지 않은지 로직을 재점검합니다.
삼항연산자를 이용합니다.

### switch문 대체하기
```jsx
// bad
function getSound(animal) {
  if (animal === '개') return '멍멍!';
  if (animal === '고양이') return '야옹~';
  if (animal === '참새') return '짹짹';
  if (animal === '비둘기') return '구구 구 구';
  return '...?';
}

console.log(getSound('개')); // 멍멍!
console.log(getSound('비둘기')); // 구구 구 구


// good
function getSound(animal) {
  const sounds = {
    개: '멍멍!',
    고양이: '야옹~',
    참새: '짹짹',
    비둘기: '구구 구 구'
  };
  return sounds[animal] || '...?';
}

console.log(getSound('개')); // 멍멍!
console.log(getSound('비둘기')); // 구구 구 구
```

## forEach, find, some, map 등 내장함수 200% 활용하기

```jsx
// this is same as
array.map((item) => addNumber(item));

// this!
array.map(addNumber);
```

## return 트릭

```jsx
const isFish = pet as Fish
const isBird = pet as Bird

// 둘 중 하나라도 true라면 true, 둘 다 false라면 false
const isTrue = () => {
    return isFish || isBird
}

```

## 변수 관련

정확한 이름을 사용합니다. 변수명을 절대로 대충 짓지 않습니다.
발음할 수 있고, 누가봐도 무엇을 뜻하는지 알 수 있는 이름이어야합니다.

```jsx
const asdf; // X
const hey; // x
const users; // O
```

2개 이상의 변수를 넣지 않습니다.
두 개 이상이 되는경우, 변수를 합치거나, 함수를 나눕니다.
객체를 변수로 지정하는 문법들에 대해서는 구조화 할당*分割代入https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment* 에 대해서 알아보세요. 여기서는 문법 자체에 대한 설명은 생략하겠습니다.

```jsx
// bad
const tooMuchParams = (foo, bar, zoo, hoge) => {
  console.log(foo, bar, zoo, hoge);
};

// good
const options = { foo, bar, zoo, hoge };
const oneParams = ({ options }) => {
  console.log({ options });
};
```

```jsx
// bad
const a = foo[0];
const b = foo[1];

// good
const [a, b] = foo;
```

### 비구조화 할당
```jsx

const inputs = {name: '', nickname:''}
const {name, nickname} =  inputs

```
## console.log() 활용하기

### console.table

### console.log({foo})

## 마지막으로
클린코드 책을 읽어보면 클린 코드를 향한 길은 굉장히 어렵다고 강조하고 있습니다. 실제로도 클린코드 책 내용도 전체적인 가이드라인이 실려있지만 당장 내 코드에 어떻게 적용하면 좋을지는 모를 때가 많았습니다. 

## 참고자료
### Youtube
- [Why I Don't Use Else When Programming](https://www.youtube.com/watch?v=EumXak7TyQ0)

### ウェブサイト
- [Is it safe to split long JavaScript if conditions into multiple lines?](https://stackoverflow.com/questions/29154339/is-it-safe-to-split-long-javascript-if-conditions-into-multiple-lines)
- https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment
- https://github.com/ryanmcdermott/clean-code-javascript
### 書籍

