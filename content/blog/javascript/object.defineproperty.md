---
title: Object.defineProperty
date: 2020-03-27 02:03:57
category: javascript
---

`Object.defineProperty()`와 점 표기법을 사용하여 값을 할당하는 것은 차이가 있다.

**1.점 표기법을 사용한 값 할당**

    var o = {};
    
    o.a = 1;
    // 아래와 같다.
    Object.defineProperty(o, 'a', {
    	value: 1,
    	writable: true,
    	configurable: true,
    	enumerable: true
    });

⇒ 점 표기법을 사용하여 값을 할당하는 경우에는 writable, configurable, enumerable이 모두 true로 define 된다.

**2. `Object.defineProperty()` 을 사용하여 값을 정의**

    var o = {};
    
    Object.defineProperty(o, 'a', { value: 1 });
    // 아래와 같다.
    Object.defineProperty(o, 'a', {
    	value: 1,
    	writable: false,
    	configurable: false,
    	enumerable: false
    });

⇒ `Object.defineProperty()` 을 사용하여 값을 정의하는 경우에는 writable, configurable, enumerable이 모두 false로 define된다.

### 커스텀 get, set 메서드

Object.defineProperty는 get, set 메서드를 커스텀할 수 있다.

*🙋‍♂️ 그럼 기본으로 제공되는 get, set 메서드가 있다는 것인가?*

    function Archiver() {
      var temperature = null;
      var archive = [];
    
      Object.defineProperty(this, 'temperature', {
        get() {
          console.log('get!');
          return temperature;
        },
        set(value) {
          temperature = value;
          archive.push({ val: temperature });
        }
      });
    
      this.getArchive = function() { return archive; };
    }
    
    var arc = new Archiver();
    arc.temperature; // 'get!'
    arc.temperature = 11;
    arc.temperature = 13;
    arc.getArchive(); // [{ val: 11 }, { val: 13 }]

- `arc.temperature` 를 실행하면, get메서드가 실행되며, 지역변수인 temperature의 값이 출력된다.
- `arc.temperature = 11` 를 실행하면, set메서드가 실행된다.

## 질문

1. enumerable이 정확히 무엇을 하는 속성인가?
2. writable과 configurable의 정확한 차이는?
