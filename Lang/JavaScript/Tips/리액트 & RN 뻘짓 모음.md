
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

## 라이브러리 관련

### react-ble-manager vs react-ble-plx

 > [!warning] react-ble-manager는 expo를 지원하지 않는다!!!
 
 - 기본적으로 큰 차이는 없음.
 - 자세한 비교 분석 기사는 [여기](https://velog.io/@mementomori/React-Native-BLE-library-%EB%B9%84%EA%B5%90react-native-ble-plx-VS-react-native-ble-manager)


## 빌드 관련
### RN Expo 안드로이드 빌드 시
#### 경위

`npx expo run:android`를 실행했는데 다음과 같은 에러가 발생
``
```
› Building app...
Configuration on demand is an incubating feature.

FAILURE: Build failed with an exception.

* What went wrong:
Could not determine the dependencies of task ':app:compileDebugJavaWithJavac'.
> Could not determine the dependencies of null.
   > SDK location not found. Define a valid SDK location with an ANDROID_HOME environment variable or by setting the sdk.dir path in your project's local properties file at  '/Users/*username*/Documents/works/rn-bluetooth/android/local.properties'.
```

#### 해결
android 폴더에 `local.properties`라는 파일을 만들고 다음 한 줄을 추가
`sdk.dir=/Users/유저이름/Library/Android/sdk`