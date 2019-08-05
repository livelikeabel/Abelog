---
title: "RxJS 기초, 핵심 \U0001F409"
date: 2019-08-05 22:08:77
category: RxJS
---

RxJS에는 4가지 핵심이 있다. 처음보고 바로 이해하기 어렵기에 일단 무작정 외우고, 자주 보고 개발 하면서 점차 이해하면 좋을것 같다.

>  Observable, Operator, Observer, Subscription

<br>

**Observable**

​	1) 시간을 축으로 연속적인 데이터를 저장하는 컬렉션을 표현한 객체

​	2) 데이터를 제공하는 소스를 Observer에게 전달한다.

<br>

**Operator**

​	1) observable을 생성 및 조작하는 함수.

​	2) 현재의 Observable 인스턴스를 기반으로 항상 새로운 Observable 인스턴스를 반환한다.

<br>

**Observer**

​	1) Observable에 의해 전달된 데이터를 소비하는 주체.

​	2) next, error, complete 함수를 가진 객체이다.

​	3) 데이터 전달시에는 next, 에러시에는 error, 데이터 전달 완료시에는 complete 함수가 호출된다.

​	4) Observable과 subscribe 메소드를 통해 연결된다. 

```js
const observer = {
	next: x => console.log(x),
	error: err => console.err(err),
	complete: ()=> console.log(‘done’)
} ;

click$.subscribe(observer);
```

<br>

**Subscription**

​	1) Observable.prototype.subscribe의 반환 값.

​	2) 자원의 해제를 담당.

​	3) 데이터를 더이상 전달받고 싶지 않을 경우 unsubscribe 메소드로 자원을 해지.

```js
const subscription = click$.subscribe(observer);
subscription.unsubscribe();
```

<br>

### RxJS 개발 프로세스 ⚙️

> 이것 역시 외운다..! 결국 이 사이클로 RxJS를 사용하니까.

1. 데이터 소스를 Observable로 변경한다. (from, of, fromEvent…)

2. 오퍼레이터를 통해 데이터를 변경하거나 추출한다.

   - 또는 여러개의 Observable을 하나의 Observable로 합치거나

   - 하나의 Observable을 여러 개의 Observable로 만든다.

3. 원하는 데이터를 받아 처리하는 Observer를 만든다.

4. Observable의 subscribe를 통해 Observer를 등록한다.

5. Observable 구독을 정지하고 자원을 해지한다.