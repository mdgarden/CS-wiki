객체를 포함한 두 배열간에 중복하지 않는 요소만 찾아내기

```jsx
const Array1 = [{id:1, name:"A"}, {id:2,name"B"}]
const Array2 = [{user_id:1, name:"A"}, {user_id:2,name:"B"},{user_id:3,name:"C"}]

const newItems = Array1.filter(({id}) => !Array2.some(({user_id})=> id === user_id));

console.log([{id:1, name:"A"}, {id:2,name"B"}])
```