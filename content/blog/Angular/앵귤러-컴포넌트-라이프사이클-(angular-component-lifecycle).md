---
title: 앵귤러 컴포넌트 라이프사이클 (Angular Component Lifecycle)
date: 2019-09-21 23:09:87
category: angular
---

# 라이프싸이클 후킹

### 라이프싸이클 함수 실행 순서

 **0. constructor**

- 컴포넌트나 디렉티브가 생성된 후에는 **생성자**가 제일 먼저 실행된다.

1. **ngOnChanges()**
    - 입력 프로퍼티 값(@Input)을 설정할 때 실행된다. (입력 프로퍼티 값이 모두 반영된 이후)
    - 입력 프로퍼티 값이 바뀔때마다 실행된다.
    - 이전 값과 현재 값을 확인할 수 있다.
    - ngOnInit()함수가 실행되기 전에 먼저 실행된다.

        ngOnChanges(changes: SimpleChanges) {
          for (let propName in changes) {
            let chng = changes[propName];
            let cur  = JSON.stringify(chng.currentValue);
            let prev = JSON.stringify(chng.previousValue);
            this.changeLog.push(`${propName}: currentValue = ${cur}, previousValue = ${prev}`);
          }
        }

    - SimpleChange 타입의 객체를 인자로 받는다.
    - 입력 프로퍼티의 이전 값과 현재 값이 포함되어 있다.
    - @Input으로 객체가 전달되면 값은 객체의 참조값으로 할당되기에 객체 안의 내용은 Angular가 변경을 추적하지 못한다. 객체로 인자를 전달했을 때는 참조하는 주소 자체가 변경되지 않으면 변경된 것으로 처리하지 않는다.

2. **ngOnInit()**
    - 생성자 이후에 실행되어야 하는 초기화 로직이 복잡할 때(ex Ajax 요청)
    - Angular가 입력 프로퍼티 값을 설정한 이후 컴포넌트에 추가 로직이 필요할 때
    - ngOnChanges()가 처음 실행된 이후에 한 번만 실행

3.  **ngDoCheck()**
    - 변화 감지 싸이클을 수동으로 실행할 때 사용
    - 변화 감지 싸이클이 실행될 때마다 실행된다.
    - ngOnChanges()와 ngOnInit() 메소드가 실행된 직후에 한 번 실행된다.
    - Angular가 감지하지 못하는 변화를 감지하는 용도로 사용한다.
    - 꼭 필요한 곳에만, 최대한 간단하게 작성한다.(너무 많이 실행되기 때문에)

4. **ngAfterContentInit()**
    - 컴포넌트의 템플릿을 컴포넌트 뷰로 준비하거나 뷰 안에 있는 디렉티브를 준비한 이후에 실행된다.
    - ngDoCheck()가 처음 실행된 직후에 한 번만 실행된다.

5. **ngAfterContentChecked()**
    - 디렉티브나 컴포넌트의 뷰를 검사한 이후에 실행된다.
    - ngAfterContentInit()이 실행된 후에 실행된다.
    - ngDoCheck() 함수가 실행된 후에 실행된다.

6. **ngAfterViewInit()**
    - 컴포넌트 뷰와 자식 컴포넌트 뷰, 뷰 안에 있는 디렉티브가 준비되었는지 검사한 후 실행

7. **ngOnDestroy()**
    - 디렉티브나 컴포넌트가 종료되기 직전에 실행
    - 옵저버블 구독해제, 이벤트 핸들러를 제거해서 메모리 누수 방지
    - 컴포넌트가 종료되는 것을 애플리케이션의 다른 부분에 전파할 수 있는 시점

### TIP

- OnChanges, DoCheck, AfterContentChecked, AfterViewChecked 에는 간결한 로직만 작성하는 것이 좋다.
- 라이프싸이클 후킹 함수를 활용하면 컴포넌트에서 생성하는 DOM 객체에 직접 접근할 수 있다.(수정 x , DOM객체 확인만 가능)
- 디렉티브가 생성되고 종료되는 시점은 디렉티브가 적용된 엘리먼트가 생성되고 종료되는 시점과 같다.

        <div *ngFor="let hero of heroes" mySpy class="heroes">
          {{hero}}
        </div>

- 컴포넌트 생성자는 최대한 간결하게 작성한다.

    [Misko Hevery(angular 팀 리더)가 말하는 생성자를 간단히 작성해야하는 이유](http://misko.hevery.com/code-reviewers-guide/flaw-constructor-does-real-work/)

    서버에서 데이터를 받아오는 로직은 컴포넌트 생성자에서 작성하지 않는다.