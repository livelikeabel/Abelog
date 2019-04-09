---
title: Map, Reduce 정복하기
date: 2019-04-08 15:04:88
category: development
---

map과 reduce는 js의 배열 메소드 중 가장 유용하고, 자주 쓰는 메소드이다. 좀 더 정확한 사용법이 궁금해져서, 따로 기록을 해보려고 한다.

## map

> Array.prototype.map

### 기본 개념

- 배열의 모든 요소를 이터레이션 하며 인자로 넘긴 콜백함수를 호출한 결과 값을 모아, 새로운 배열에 넣어 반환한다.

`arr.map(callback(currentValue[, index[, array]])[, thisArg])`

map의 매개변수로는, 새로운 배열 요소를 생성하는 `callback`함수와, callback을 실행할 때 this로 사용되는 `thisArg`가 있다.
callback함수는 인자로 currentValue, index, array를 갖는다.

### 특징

- `map`은 호출한 배열의 값을 변형하지 않는다. 단, `callback` 함수에 의해서 변형될 수는 있다.
- `map`이 처리할 요소의 범위는 첫 callback을 호출하기 전에 정해진다. `map`이 시작한 이후 배열에 추가되는 요소들은 callback을 호출하지 않는다. 배열에 존재하는 요소들의 값이 바뀐 경우, `map`이 방문하는 시점의 값이 callback에 전달된다. map이 시작되고, 방문하기 전에 삭제된 요소들은 방문하지 않는다.
- `map`을 호출한 배열의 중간이 비어있는 경우, 결과 배열 또한 동일한 인덱스를 빈 값으로 유지한다.

### 신기한 use case

#### 1. `String`에서 map 사용하기

map은 array의 메소드이기 때문에 String에 map함수를 사용하면 `not a function`에러가 발생한다. 그런데 아래와 같은 방법을 사용하면 가능하다.

```js
var map = Array.prototype.map
var a = map.call('Hello Abel', v => v.charCodeAt(0))
// [72, 101, 108, 108, 111, 32, 65, 98, 101, 108]
```

1. Array.prototype의 map 함수를 map이라는 변수에 할당한다.
2. map을 call 함수를 통해서 실행시킬때 첫번째 인자로 this로 사용할 String을 넣고, 두번째 인자로는 callback함수를 넘긴다.
3. String은 ArrayLike(유사배열)이기 때문에 map함수가 돌아간다! 😎
   > 근데 이제 우리에게는 `...`(spread operator)가 있기 때문에
   >
   > ```
   > [...ArrayLike].map(v => v)
   > ```
   >
   > 이렇게 하는게 간결할거 같다... ㅎㅎ

#### 2. map의 콜백함수가 두개 이상의 인자를 받는 경우

```
['1', '2', '3'].map(parseInt)
// [1, NaN, NaN]
```

기대하는 값은 `[1,2,3]`이였는데, 원치 않는 결과가 나왔다.
parseInt는 두개의 인자(value, 진법)를 받을 수 있고, map은 콜백함수에게 세개의 인자(value, index, array)를 넘긴다. 암묵적으로 map이 두번째 인자로 index로 넘기고, parseInt가 그 index를 진법으로 인식해서 원치않는 오류가 난 것이다.

```
['1', '2', '3'].map(str => parseInt(str))
// [1, 2, 3]
```

위와 같이 하나만 넘겨주면 깔끔!

출처:

- https://github.com/livelikeabel/AbelKo
- https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/map
