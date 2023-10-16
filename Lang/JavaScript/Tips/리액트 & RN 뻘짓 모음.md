
## 컴포넌트 관련 

엑스포에서 핫리로드가 안돼서 엥 ㅠㅠ 왜 ㅠㅠ 했는데
```jsx
{isConnected ? Scanning() : Connected()}
```

이게 아니고

```jsx
{isConnected ? <Scanning /> : <Connected />}
```
이렇게 컴포넌트로 돌려줘야했음...
근데 왜지 ㅠ 업무에서는 그냥 위쪽 방법으로 썼던 것 같은데 ㅠㅠ 


## hooks 관련

### 훅이 길어질 때 따로 빼기

훅 파일

```javascript
export const useHook = () => {

  const function1 = () => {
  // logic here
  };

  const function2 = () => {
  // logic here
  };

  return {function1, function2};
};
```

화면에서 사용할 때
```javascript
const {function1, function2} = useHook();
```