---
title: web의 다양한 Redirect 구현
date: 2019-04-04 21:04:72
category: development
---

redirect의 뜻은 영어단어 그대로이다. `Redirect: 다시 향하게 하다 새 방향으로 돌리다.`
여러가지 redirect 방법이 있다 하나씩 살펴보자.

1. window.location.href

`herf` 메소드를 이용해서 특정 URL로 접속시 다른 URL로 이동시킬 수 있다.
```js
window.location.href = 'https://abelog.netlify.com/';
```
> 웹브라우저로 접속시에 'https://abelog.netlify.com/'로 이동시킨다.



HTTP에서, 리다이렉션



리다이렉션을 명시하는 대체 방법.
- <meta> (HTML 리다이렉션)


- DOM (Javascript 리다이렉션)


---
### 참고
https://developer.mozilla.org/ko/docs/Web/HTTP/Redirections