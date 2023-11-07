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