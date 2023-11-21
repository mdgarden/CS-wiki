## 1.6 リテラルを使って値を生成

```js
var myNumber = new Number(23); // 숫자 오브젝트 (실제 코딩에서는 비추천)
var myNumberLiteral = 23; // 객체가 아닌 원시값
```

일반적으로 JavaScript의 리테랄은 new 연산자가 하는 것을 숨기고 있는 것에 불과함. 더욱 중요한 것은 리테랄은 new 연산자와 생성자 함수를 사용하는 오브젝트 생성과 비교해서 편리하다는 점임

> [!note]
> 문자열, 수치, 불리언을 리테랄로 기술하면 원시값으로 생성되어, 생성된 값이 오브젝트처럼 쓰일 때까지는 오브젝트가 생성되지 않는다. "오브젝트처럼 쓰인다"라는 것은, 그 원시값에 대응하는 생성자 함수가 가지는 메소드를 사용하려고 한다던가, 프로파티를 취득하려고 하는 것으로 (예: 'var charctersInFoo = 'foo'.length), 그것이 발생할 때까지는 원시값으로서 취급된다. 

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

> [!abstract] Abstract, Summary, Tldr
> 원시값은 JavaScript의 세계에서 가장 낮은 레이어 단위임
> 원시값은 객체가 아님

## 1.11 プリミティブ型の文字列、数値、真偽値はオブジェクトのように扱うとオブジェクトのようにふるまう
셀프보충)
### 원시 값

[JavaScript](https://developer.mozilla.org/ko/docs/Glossary/JavaScript)에서, **원시 값**(primitive, 또는 원시 자료형)이란 [객체](https://developer.mozilla.org/ko/docs/Glossary/Object)가 아니면서 [메서드](https://developer.mozilla.org/ko/docs/Glossary/Method) 또는 [속성](https://developer.mozilla.org/ko/docs/Glossary/Property/JavaScript)도 가지지 않는 데이터입니다. 원시 값에는 7가지의 종류가 있습니다. [출처](https://developer.mozilla.org/ko/docs/Glossary/Primitive)
원시값 string과 객체 string은 다르다는 뜻