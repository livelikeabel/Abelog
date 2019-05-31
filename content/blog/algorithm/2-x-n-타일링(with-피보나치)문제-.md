---
title: 2 x n 타일링(with 피보나치)문제 
date: 2019-05-31 17:05:05
category: algorithm
---

[문제 보러가기](https://programmers.co.kr/learn/courses/30/lessons/12900#)

처음에 어찌 풀어야 할지 몰라서, 종이에다 막 그렸다.<br>
결국, 감이 안와서 제로초님의 블로그를 보고 `피보나치 수열`을 이용해서 접근해야 한다는 것을 알았다.

피보나치 수열이 뭔지 기억이 1도 안나서 [위키 - 피보나치 수열](https://ko.wikipedia.org/wiki/%ED%94%BC%EB%B3%B4%EB%82%98%EC%B9%98_%EC%88%98)을 검색했다.

피보나치 수열을 간단히 말하면,
> 첫째 및 둘째 항이 1이며 그 뒤의 모든 항은 바로 앞 두 항의 합인 수의 나열

이다.

### 문제를 보자

n이 1일 때는 타일의 모양은 세로로 <u>1개</u>이다. `|`<br>
n이 2일 때는 `||` , `=`  <u>2개</u>이다. <br>
n이 3일 때는 `|||` , `=|` , `|=` <u>3개</u>이다. <br>
n이 4일 때는 `||=` , `|=|` , `||=`, `=||`, `==` <u>5개</u> 이다.<br>
.<br>
.<br>
.<br>
n이 5일 때는 8개<br>
n이 6일 때는 13개


규칙을 찾으면, 
`n = n-1 + n-2`
와 같은 피보나치 수열을 이용한 것이 보인다.


### 완성된 `titling` 함수

```js
function tiling(n) {
  const memo = [1, 2];    
  for(let i = 2; i < n; i++) {
      memo[i] =(memo[i-1] + memo[i-2]) % 1000000007;
  }
  return memo[n-1]
}
```

이렇게 풀면 된다 :)

출처: [zerocho 블로그 - 프로그래머스 알고리즘](https://www.zerocho.com/category/Algorithm/post/5b87ccc1553b47001bb08d2b)






