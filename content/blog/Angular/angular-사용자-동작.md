---
title: Angular 사용자 동작
date: 2019-09-16 22:09:29
category: angular
---
# 사용자 동작

### $event 객체의 타입

    export class KeyUpComponent_v1 {
      values = '';
    
    
      onKey(event: KeyboardEvent) { // 타입을 지정한 경우
        this.values += (<HTMLInputElement>event.target).value + ' | ';
      }
    }

$event 객체를 KeyboardEvent 타입으로 지정했다. 이 이벤트의 target 프로퍼티는 입력 필드라는 것이 명확해졌다. onKey 메소드는 템플릿에서 어떤 타입의 인자를 받아야 하는지 더 확실해졌고, 이 인자를 어떻게 활용할 수 있는지에 대해서도 더 많은 정보를 제공할 수 있게 되었다.

⇒ 이벤트에도 타입을 명시해 주는 것이 좋다.

더 간단하게 할 수 있다.

    @Component({
      selector: 'app-key-up2',
      template: `
        <input #box (keyup)="onKey(box.value)">
        <p>{{values}}</p>
      `
    })
    export class KeyUpComponent_v2 {
      values = '';
      onKey(value: string) {
        this.values += value + ' | ';
      }
    }

⇒ 컴포넌트에서 다른 것은 신경쓰지 않고 입력 필드의 데이터만 받을 수 있기에 좋다. $event 객체의 타입에 신결쓸 필요가 없다.

### 키 입력 필터링 (key.enter)

keyup.enter라고 바인딩하면 엔터키가 입력되었을 때만 이벤트 핸들러를 실행할 수 있다.

    @Component({
      selector: 'app-key-up3',
      template: `
        <input #box (keyup.enter)="onEnter(box.value)">
        <p>{{value}}</p>
      `
    })
    export class KeyUpComponent_v3 {
      value = '';
      onEnter(value: string) { this.value = value; }
    }

### Tip

- 엘리먼트 대신 템플릿 변수 사용하기
- 엘리먼트를 전달하지 말고 값을 전달하기
- 템플릿 실행문은 간단하게 작성하기
