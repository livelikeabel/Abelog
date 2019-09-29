---
title: Angular에서 옵저버블 활용하기
date: 2019-09-29 22:09:87
category: angular
---

# Angular에서 옵저버블 활용하기

angular는 비동기 로직을 처리할 때 옵저버블을 다양하게 사용한다.

- Observable 클래스를 상속해서 EventEmitter 클래스를 제공한다.
- HTTP 모듈이 AJAX 요청을 보내거나 응답을 받아 처리할 때 옵저버블을 사용한다.
- 라우터와 폼 모듈이 사용자 입력 이벤트를 감지할 때 옵저버블을 사용한다.

### 이벤트 이미터(Event Emitter)

- EventEmitter 클래스는 컴포넌트에서 @Output 데코레이터로 지정된 프로퍼티가 컴포넌트 외부로 데이터를 보낼 때 사용한다.
- **Observable 클래스를 상속받아 구현**되었다.
- `emit()` 메소드로 데이터를 내보낸다. `emit()` 을 실행하면서 전달한 인자는 **옵저버블의 `next()`메소드로 전달**된다.

        export class EventEmitter<T extends any> extends Subject<T> {
        	...
        	emit(value?: T) { super.next(value); }
        	...
        	const sink = super.subscribe(schedulerFn, errorFn, completeFn);
        	
          return sink;
        }

### HTTP

- Angular에서 제공하는 HttpClient는 HTTP 요청 결과를 옵저버블로 반환한다.
    - `http.get(`api`)`를 실행한 결과는 옵저버블이다.
- 옵저버블을 사용하는 방식이 좋은 점
    1. 옵저버블은 서버에서 받은 응답을 **다른 객체로 변환하지 않는다**. Promise를 사용하면 .then()으로 체이닝 할때마다 새로운 객체가 생성되는 것과 다르다.
    2. `unsubscribe()` 메소드를 사용하면 아직 완료되지 않은 **HTTP 요청을 취소**할 수 있다.
    3. 서버의 **응답 진행률을 확인**할 수 있다.
    4. 실패한 요청을 간단하게 재시도 할 수 있다.

### Async 파이프

- 옵저버블이나 Promise를 구독하고, 이 객체가 담고 있는 마지막 값을 반환한다. 그리고 새로운 값이 전달되면 컴포넌트가 변화를 감지하도록 알린다.

### Router

- `Router.events`는 라우팅 이벤트를 옵저버블로 전달한다.
- 필요한 이벤트만 처리하려면 RxJS의 `filter()` 연산자를 사용한다.

        navStart$: Observable<NavigationStart>;
        
        constructor(private router: Router) {
        	this.navStart$ = router.events.pipe(
        		filter(evt => evt instanceof NavigationStart)
        	) as Observable<NavigationStart>;
        }
        
        ngOnInit() {
        	this.navStart$.subscribe(evt => console.log('Navigation Started!'));
        }

- ActivatedRoute도 현재 라우팅 경로나 라우팅 인자를 옵저버블로 제공한다. `ActivateRoute.url`을 구독하면 현재 라우팅 경로를 얻을 수 있다.

        constructor(private activatedRoute: ActivatedRoute) {}
        
        ngOnInit() {
        	this.activatedRoute.url
        		.subsribe(url => console.log('The URL changed to:' + url));
        }

질문

- 라우팅 관련해서 어떤 상황에 어떤 걸 사용해야 하나...?

    앵귤러 자체의 라우팅도 있고, ngrx에서 제공하는 것도 있는데... 무슨 차이 일까..? 왜 ngrx에서 라우팅을 지원하는 걸까...? (effect 중간에 route 정보를 알고 싶어서?)

### 반응형 폼

- `FormControl`의 프로퍼티 중 `valueChanges`와 `statusChanges` 를 구독하면 폼 컨트롤의 값과 상태가 변하는 것을 확인할 수 있다.

        logNameChange() {
        	const nameControl = this.heroForm.get('name');
        	nameControl.valueChanges.forEach(v => this.nameChangeLog.push(v));
        }


출처: 앵귤러 공식문서