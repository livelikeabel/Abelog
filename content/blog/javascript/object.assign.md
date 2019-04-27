---
title: Object.assign
date: 2019-04-27 13:04:05
category: javascript
---
첫번째 인자는 target, 두번째 인자부터는 객체가 들어와서 뒤에있는 객체들의 키들을 계속 타겟으로 옮겨줘서 타겟을 리턴하는 함수.
> The Object.assign() method is used to copy the values of all enumerable own properties from one or more source objects to a target object. It will return the target object.

### 동작예시
```js
const target = { a: 1, b: 2 };
const source = { b: 4, c: 5 };

const returnedTarget = Object.assign(target, source);

console.log(target);
// expected output: Object { a: 1, b: 4, c: 5 }

console.log(returnedTarget);
// expected output: Object { a: 1, b: 4, c: 5 }
```

- 동일한 키가 존재할 경우 target 객체의 속성은 source 객체의 속성으로 덮어쓰여진다.
- 열거할 수 있는 source 객체의 속성만 target 객체로 복사한다.
- source 객체의 `[[Get]]`, target 객체의 `[[Set]]` 을 사용하여 getter 와 setter 를 호출한다.
- 속성을 단순히 복사하거나 새롭게 정의하는 것이 아니라 할당하는 것이다.
- 병합가능 `Object.assign(o1, o2, o3);`
- 속성은 파라미터 순서에서 더 뒤에 위치한 동일한 속성을 가진 다른 객체에 의해 덮어쓰인다.

### object clone
```js
const obj = { a: 1 };
const copy = Object.assign({}, obj);
console.log(copy); // { a: 1 }
```

- **얕은 복사만 수행한다. 깊은 복사는 되지 않음.**
```js
let obj1 = { a: 0 , b: { c: 0}};
  let obj2 = Object.assign({}, obj1);
  console.log(JSON.stringify(obj2)); // { a: 0, b: { c: 0}}
  
  obj1.a = 1;
  console.log(JSON.stringify(obj1)); // { a: 1, b: { c: 0}}
  console.log(JSON.stringify(obj2)); // { a: 0, b: { c: 0}}
  
  obj2.a = 2;
  console.log(JSON.stringify(obj1)); // { a: 1, b: { c: 0}}
  console.log(JSON.stringify(obj2)); // { a: 2, b: { c: 0}}
  
  obj2.b.c = 3; // obj1, obj2 모두에 영향을 줌
  console.log(JSON.stringify(obj1)); // { a: 1, b: { c: 3}}
  console.log(JSON.stringify(obj2)); // { a: 2, b: { c: 3}}
```
- **깊은 복사 하기**
```js
JSON.parse(JSON.stringify(obj1));
```
> 좋은 방법일까...? C로 돌려서 빠르긴 한다던데... 깊은 복사를 해야할 일이 생긴다면 이렇게 하는걸 추천한다고 하네엽..!


#### 출처 👇🏽
https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Object/assign