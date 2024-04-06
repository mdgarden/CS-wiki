---
tags:
  - "#JavaScript/Array"
---

객체를 포함한 두 배열간에 중복하지 않는 요소만 찾아내기

```jsx
const Array1 = [{id:1, name:"A"}, {id:2,name"B"}]
const Array2 = [{user_id:1, name:"A"}, {user_id:2,name:"B"},{user_id:3,name:"C"}]

const newItems = Array1.filter(({id}) => !Array2.some(({user_id})=> id === user_id));

console.log([{id:1, name:"A"}, {id:2,name"B"}])
```

배열 만드는 여러가지 방법

```ts
const arr: number[] = new Array(nums.length+1).fill(0);
const arr = Array.from({length: nums.length} (v, i) => i) // [0, 1, 2...]
```

https://gist.github.com/mdgarden/c8b662bf2875faf5607a3952e96e17be