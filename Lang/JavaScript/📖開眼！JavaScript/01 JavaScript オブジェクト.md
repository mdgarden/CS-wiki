## 1.7 プリミティブ型（基本型）の値
```js
var myString = 'string';
var myNumber = 5;
var myBoolean = true;
var myNull = null;
var myUndefined = undefined;

console.log(myString, myNumber, myBoolean, myNull, myUndefined); 
// "string", 5, true, null, undefined

var myObject = {
	myString: 'string',
  myNumber: 10,
  myBoolean: false,
  myNull:null,
  myUndefined: undefined,
}

console.log(myObject)
// { myBoolean: false, myNull: null, myNumber: 10, myString: "string", myUndefined: undefined }

var myArray = ['string', 10, false, null, undefined];
console.log(myArray);
// ["string", 10, false, null, undefined]
```

## 1.11
셀프보충)
# 원시 값

[JavaScript](https://developer.mozilla.org/ko/docs/Glossary/JavaScript)에서, **원시 값**(primitive, 또는 원시 자료형)이란 [객체](https://developer.mozilla.org/ko/docs/Glossary/Object)가 아니면서 [메서드](https://developer.mozilla.org/ko/docs/Glossary/Method) 또는 [속성](https://developer.mozilla.org/ko/docs/Glossary/Property/JavaScript)도 가지지 않는 데이터입니다. 원시 값에는 7가지의 종류가 있습니다.
https://developer.mozilla.org/ko/docs/Glossary/Primitive
원시값 string과 객체 string은 다르다는 뜻