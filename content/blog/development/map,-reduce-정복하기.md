---
title: Map, Reduce 정복하기
date: 2019-04-08 15:04:88
category: development
---

map과 reduce는 js의 배열 메소드 중 가장 유용하고, 자주 쓰는 메소드이다. 좀 더 정확한 사용법이 궁금해져서, 따로 기록을 해보려고 한다.

결론부터 이야기 하면, 배열에 있는 고차함수를 쓰는 원리는 간단하다.

**배열을 루프돌고 싶으면, `forEach` 배열의 원소를 바꾼 배열을 얻고 싶으면, `map` 하나의 값으로 뭉치고 싶으면 `reduce`를 쓰면된다.**

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

## reduce

`reduce()` 메서드는 배열의 각 요소에 대해 주어진 reducer 함수를 실행하고, 하나의 결과값을 반환한다.

```js
const reduer = (acc, cur, i, arr) => return `result_value`
arr.reduce(reducer, initialValue);
```

#### reduce는 reducer 함수와 initialValue를 인자로 받는다.

1. reducer는 네 개의 인자를 가진다.

```
1. 누산기(accumulator) - 콜백의 반환값이 누적된다.
2. 현재 값
3. 현재 인덱스 - `initialValue`를 제공한 경우 0, 아니면 1부터 시작한다.
4. 원본 배열
```

=> 리듀서 함수의 반환 값은 누산기(acc)에 할당되고, 누산기는 순회 중 **유지**되므로 최종 결과는 <u>**하나의 값**</u>이 된다.

2. initialValue

- acc에 초기값을 제공한다. 초기값이 없으면 배열의 첫번째 요소를 사용한다.
- 빈 배열에서 초기값 없이 `reduce()`를 호출하면 오류가 발생한다. 초기값을 주는게 안전하다.

### reduce 활용

#### 중첩 배열 펼치기(flatten)

```js
const flattended = [[0, 1], [2, 3], [4, 5]].reduce(
  (acc, cur) => acc.concat(cur),
  []
)
```

> [concat()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/concat) : 인자로 주어진 배열이나 값들을 기존 배열에 합쳐서 새 배열을 반환합니다.

#### 배열의 중복 항목 제거하기

```js
let arr = [1, 2, 1, 2, 3, 5, 4, 5, 3, 4, 4, 4, 4]

arr.sort().reduce((acc, cur) => {
  const length = acc.length
  if (length === 0 || acc[length - 1] !== cur) {
    acc.push(cur)
  }
  return acc
}, [])
// [1, 2, 3, 4, 5]
```

> - 좋은 중복제거 방법인가....? 예외 처리할게 너무 많다... 하지만 reduce로는 거의 상상한 모든것을 할 수 있다는 것을 느낀다.
> - 초간단한 배열의 중복 제거 방법! : `[...new Set(arr)]`

#### 함수 구성을 위한 파이프 함수

```js
const double = x => x + x
const triple = x => 3 * x

const pipe = (...functions) => input =>
  functions.reduce((acc, fn) => fn(acc), input)

const multiply6 = pipe(
  double,
  triple
)
multiply6(6) // 36
```

=> reduce를 통해 pipe 함수를 만들 수 있다!

출처:

- https://github.com/livelikeabel/AbelKo
- https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/map
- https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce
- https://www.youtube.com/watch?v=_JGchAMbPGI&list=PLBNdLLaRx_rKT18ivygZ7Jmi_4h5zb2wv
