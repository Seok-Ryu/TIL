# ES6 문법
잘 모르던 또는 헷갈리던 ES6문법들에 대한 정리

##for-of
기존 `for-in`이 상위 prototype 요소도 포함 된다는 문제를 해결

```javascript
//for-in
var data = ["irodog", "roodig"];
Array.prototype.getIndex = "godori";

for(let idx in data){
    console.log(data[idx]); // irodog, roodig, godori
}
    
//for-of    
var data = ["irodog", "roodig"];
Array.prototype.getIndex = "godori";

for(let value of data){
    console.log(value); // irodog, roodig
}
```

## spread 연산자
`...array` 형태로 사용. 배열요소를 순차적으로 접근하여 전개 return? 

```javascript
let data = ["godori", "irodog", "roodig"];
let newData = [...data];
console.log( newData === data );  // false

function sum(a,b,c){
    return a+b+c;
}
let arr = [100,200,300];
console.log( sum(...arr) );


function sum(...arr) {
  return arr.length;
}
console.log(sum(1,2,3,4)); //4 
```

## object 선언시 key 생략

```javascript
return {
            getName : getName,
            setName : setName
        };
        
return {getName, setName};
```

##  Object, array 로부터 변수 할당
```javascript
let arr = ['aaa','bbb', 'ccc'];
let [a, , c] = arr;
console.log(a, c) //'aaa', 'ccc'


let obj = {name: 'abcd', age: 1234};
let {name, age} = obj; // let name = obj.name, age = obj.age;
let {name:myName, age: myAge} = obj; // let myName = obj.name, myAge = obj.age;


// parameter에서도 사용 가능
function foo({name: x}) {
  console.log(x);
}
foo({name: 5})
```

## Default  
변수가 undefined 일때 변수에 default 값 할당
```javascript
function sum(x, y=12) {
  // y is 12 if not passed (or passed as undefined)
  return x + y;
}
sum(3) // 15
```

## Template Strings
기존 string 을 위한 `'`, `"` 대신 ``(backtick) 를 사용가능
```javascript
// String interpolation
let name = "Bob", time = "today";
let hello = `Hello ${name}, how are you ${time}?`;

// Multiline strings
`In JavaScript this is
 not legal.`
 
```