---
title: Angular Component & template (앵귤러 컴포넌트 & 템플릿)
date: 2019-09-14 23:09:66
category: angular
---

### 데이터 표시하기

**ngIf**

ngIf 의 조건을 만족하지 않아서 엘리먼트가 화면에 표시되지 않을 때, 엘리먼트는 감춰지는 것이 아니고 DOM에서 완전히 제거됩니다. 이 방식은 성능 향상에 도움이 되며, 조건문이 많고 데이터 바인딩을 많이 하는 프로젝트에 더욱 유용합니다.

### 템플릿 문법

***ngFor**

tip: *ngFor를 사용하면서 trackBy 기능을 사용하면 이전과 다른 객체를 참조하더라도 같은 객체를 참조하는 것으로 간주할 수 있습니다.

**실행시간은 최대한 짧게**

Angular는 변화 감지 싸이클마다 템플릿 표현식을 다시  평가한다. 따라서 템플릿 표현식은 최대한 빠르게 완료되어야 하며, 연산이 많이 필요한 작업이라면 결과값을 캐싱하는 방법도 고려한다.

**로직은 최대한 단순하게**

프로퍼티 참조, 메소드 실행하는 정도가 좋다. 그 밖의 로직은 컴포넌트에 작성하고 템플릿에서는 실행만 한다.(개발과 테스트에 용이)

**템플릿 실행문의 컨텍스트**

    <button (click)="onSave($event)">Save</button>
    <form #heroForm (ngSubmit)="onSubmit(heroForm)"> ... </form>

- 복잡한 로직을 작성하지 않는 것이 좋다. 간단히 프로퍼티를 참조하거나 함수를 실행하는 것이 좋다.

### **HTML 어트리뷰트 vs DOM 프로퍼티**

어트리뷰트는 **HTML**에 지정하고, 프로퍼티는 **DOM**에 지정한다.

> 어트리뷰트는 DOM 프로퍼티의 초기값을 지정하고 역할이 끝난다. 값도 변하지 않는다. 프로퍼티는 값을 바꾸면서 계속 유지된다.

브라우저가 렌더링하는 

    <input type="text" value="Bob">

엘리먼트로 설명하면, 이 DOM 노드는 어트리뷰트 값인 "Bob"으로 value 프로퍼티가 초기화 되면서 만들어 진다. 그리고 사용자가 이 입력 필드에 "Sally"라고 입력하면 DOM 엘리먼트의 value 프로퍼티는 "Sally"라는 값으로 변경된다. 하지만 HTML에 있는 value 어트리뷰트는 input.getAttribute('value')로 찾아봐도 "Bob"으로 남아있다.

HTML에 있는 value 어트리뷰트는 연결된 DOM 필드의 값을 초기화할 뿐이고, DOM에 있는 value 프로퍼티가 현재값을 나타낸다.

중요한 내용이니 다시한번 말하면: **템플릿 바인딩은 *프로퍼티*나 *이벤트*와 한다. *어트리뷰트*가 아니다.**

**프로퍼티 바인딩 ( [프로퍼티] )**

- 뷰 엘리먼트의 프로퍼티를 연결하는 바인딩이다.

    <img [src]="heroImageUrl">

디렉티브 프로퍼티를 설정하려면 다음과 같이 사용한다.

    <div [ngClass]="classes">ngClass binding to the classes property</div>

> 문법적으로 보면 디렉티브의 입력 프로퍼티로 지정된 프로퍼티 중에 같은 이름인 프로퍼티에 바인딩됩니다. 이 때 바인딩을 받는 디렉티브에서는 입력값을 받기 위해 inputs 배열을 지정하거나 @Input() 데코레이터를 지정해야 합니다.

디렉티브나 엘리먼트에서 프로퍼티 이름을 찾지 못하면 “unknown directive” 에러가 발생합니다.

**프로퍼티 바인딩? 문자열 바인딩?**

    <p><span>"{{title}}" is the <i>interpolated</i> title.</span></p>
    <p>"<span [innerHTML]="title"></span>" is the <i>property bound</i> title.</p>
    
    <p><img src="{{heroImageUrl}}"> is the <i>interpolated</i> image.</p>
    <p><img [src]="heroImageUrl"> is the <i>property bound</i> image.</p>

- 문자열 바인딩이 프로퍼티 바인딩보다 편하고 가독성이 더 좋다.
- 바인딩되는 프로퍼티의 타입이 문자열이 아니라면 반드시 프로퍼티 바인딩을 사용해야한다.(angular는 템플릿에 값을 반영하기 전에 코드의 안정성을 검증한다.)

**어트리뷰트 바인딩**

- 엘리먼트의 프로퍼티 값은 어트리뷰트에 문자열로 직접 지정하는 것보다 프로퍼티 바인딩을 사용하는 것이 언제나 좋다.
- 어트리뷰트 바인딩은 지정하려는 속성이 프로퍼티에 없고 어트리뷰트에 있을 때만 사용해야한다.

    <table border=1>
      <tr><td [attr.colspan]="1 + 1">One-Two</td></tr>
      <tr><td>Five</td><td>Six</td></tr>
    </table>

    <!-- 웹 접근성을 위해 aria 어트리뷰트를 지정합니다. -->
    <button [attr.aria-label]="actionName">{{actionName}} with Aria</button>

**클래스 바인딩**

    <!-- 바인딩을 사용해서 클래스를 새롭게 덮어쓰는 설정 -->
    <div class="bad curly special"
         [class]="badCurly">Bad curly</div>
    
    
    <!-- 프로퍼티로 "special" 클래스 토글하기 -->
    <div [class.special]="isSpecial">The class binding is special</div>
    
    <!-- 클래스 프로퍼티로 `class.special` 클래스 바인딩하기 -->
    <div class="special"
         [class.special]="!isSpecial">This one is not so special</div>

[NgClass 디렉티브](https://angular.kr/guide/template-syntax#ngclass)를 사용하면 여러 클래스 중 어떤 클래스를 지정할지 자유롭게 조작할 수 있다.

**$event 객체와 이벤트 처리 실행문**

    <input [value]="currentItem.name"
           (input)="currentItem.name=$event.target.value" >
    without NgModel

이 코드에서는 `currentHero.name` 프로퍼티를 `<input>` 엘리먼트의 `value` 프로퍼티로 바인딩하면서 초기값을 지정합니다. 그리고 값이 변경되는 것을 감지하기 위해 `<input>` 엘리먼트의 `input` 이벤트를 바인딩합니다. 사용자가 입력 필드의 값을 변경하면 `input` 이벤트가 발생하고 이 이벤트에 연결된 템플릿 실행문이 실행되는데, 이 때 DOM 이벤트 객체가 `$event` 객체로 템플릿 실행문에 전달됩니다.

그리고 이벤트 객체에서 값을 참조해서 `name` 프로퍼티 값을 다시 지정하기 위해 템플릿 실행문을 `$event.target.value` 와 같이 작성했습니다.

대상 이벤트가 DOM 엘리먼트의 이벤트가 아니고 커스텀 디렉티브(컴포넌트)에서 정의하는 이벤트라면, `$event` 객체는 해당 디렉티브에서 정의하는 대로 자유로운 형식이 될 수 있습니다.

**Custom events with EventEmitter**

EventEmitter를 사용하면 커스텀 이벤트를 만들 수 있다. 디렉티브에 EventEmitter 타입의 프로퍼티를 선언하고 이 프로퍼티를 외부로 열어준다. 그런 뒤 EventEmitter객체의 emit(데이터) 함수를 실행하면 데이터가 $event 객체에 담겨 디렉티브 외부로 전달된다. 부모 디렉티브에서는 자식 디렉티브의 이벤트 프로퍼티를 바인딩해서 이 커스텀 이벤트를 감지하고 있다가, 이벤트가 발생했을 때 $event 이벤트에 담긴 데이터를 받아서 처리하면된다.

[좋은예시](https://angular.kr/guide/template-syntax#custom-events-with-eventemitter)

질문

1. [변수 초기화는 생성자에서? 클래스에서?](https://angular.kr/guide/displaying-data#%EB%B3%80%EC%88%98-%EC%B4%88%EA%B8%B0%ED%99%94%EB%8A%94-%EC%83%9D%EC%84%B1%EC%9E%90%EC%97%90%EC%84%9C-%ED%81%B4%EB%9E%98%EC%8A%A4%EC%97%90%EC%84%9C)

    [공식 문서](https://angular.kr/guide/displaying-data#%EB%B3%80%EC%88%98-%EC%B4%88%EA%B8%B0%ED%99%94%EB%8A%94-%EC%83%9D%EC%84%B1%EC%9E%90%EC%97%90%EC%84%9C-%ED%81%B4%EB%9E%98%EC%8A%A4%EC%97%90%EC%84%9C) 에서는 클래스에 변수를 선언하면서 초기값을 할당하는 것이 간결한 방식이라고 한다.

    [ngrx 공식 문서](https://ngrx.io/guide/effects)에서도 클래스에 변수를 선언하면서 초기값을 할당한다.

문제

1. 어트리뷰트와 프로퍼티의 차이는?