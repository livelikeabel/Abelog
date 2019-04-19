---
title: 'createElement, appendChild을 사용해 동적으로 테이블 만들기'
date: 2019-04-19 13:04:29
category: javascript
---

### createElement 메서드로 html 태그를 만들 수 있다.
> `createElement(‘tr’)` 을 사용하면 테이블의 열을 만드는 `<tr></tr>` 엘리먼트가 생긴다.

#### 1. `el`함수를 만들어 놓으면 좀 더 간편하게 쓸 수 있다.

```js
const el = tag => document.createElement(tag);
el('tr')
```

#### 2. tr을 만들고, td를 넣어보자. appendChild를 사용해서 넣을 수 있다.
```js
const tr = el('tr')
tr.appendChild(el('td'))

->  <tr>
      <td><td/>
    </tr>
```

#### 3. reduce함수를 사용해서 동적으로 table을 만들어보자

```js
const data = [[1,2,3],[4,5,6],[7,8,9]];
let table = document.querySelector('table')
data.forEach(row => table.appendChild(
  row.reduce((tr, n)=>{
    tr.appendChild(el('td')).innerHTML=n
    return tr
  }, el('tr'))
))
```
1. `<table id="table"></table>` 을 가져온다.
2. 이차원배열로 이루어진 data를 순회한다. 요소 하나가 테이블의 행이다.
3. data를 순회할 때, table에 appendChild로 `<tr>` 로 바뀐 행을 넣도록 한다.
4. `<tr>`을 reduce를 사용해서 만든다. el('tr')로 `<tr>`을 만들고 그안에 appendChild로 `<td>`를 넣어준다. accumulator인 `<tr>`에 `<td>`를 누적한다.