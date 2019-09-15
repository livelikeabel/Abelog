---
title: python-Function (파이썬 함수)
date: 2019-09-15 21:09:16
category: python
---

# Function

### 함수의 호출 방식

**Call by Value**

- 함수에 인자를 넘길 때 값만 넘김
- 함수 내에 인자 값 변경 시, 호출자에게 영향을 주지 않음

**Call by Reference**

- 함수에 인자를 넘길 때 메모리 주소를 넘김
- 함수 내에 인자 값 변경 시, 호출자의 값도 변경됨

파이썬은 객체의 주소가 함수로 전달되는 방식

전달된 객체를 참조하여 변경 시 호출자에게 영향을 주나, 새로운 객체를 만들 경우 호출자에게 영향을 주지 않는다.

    def spam(eggs):
        eggs.append(1)
    		eggs = [2, 3]
    
    ham = [0]
    spam(ham)
    print(ham)

**변수의 범위**

- 함수 내에서 전역변수 사용 시 global 키워드 사용

        def f():
        		global s
        		s = "I love London!"
        		print(s)
        
        s = "I love Paris!"
        f()
        print(s)
        
        # I love London! 
        # I love London!

### Recursive Function

- 자기자신을 호출하는 함수
- 점화식과 같은 재귀적 수학 모형을 표현할 때 사용
- 재귀 종료 조건 존재, 종료 조건까지 함수호출 반복

### Keyword arguments

- 함수에 입력되는 parameter의 변수명을 사용, arguments를 넘김

    def print_somthing(my_name, your_name):
    		print("Hello {0}, My name is {1}".format(your_name, my_name))
    
    print_somthing("abel", "mapia")
    print_somthing(your_name="mapia", my_name="abel")

### Default arguments

- parameter의 기본 값을 사용, 입력하지 않을 경우 기본값 출력

    def print_somthing_2(my_name, your_name="mapia"):
    		print("Hello {0}, My name is {1}".format(your_name, my_name))
    
    print_somthing_2("abel", "mapia")
    print_somthing_2("abel")

### 가변인자(Variable-length)

- 개수가 정해지지 않은 변수를 함수의 parameter로 사용하는 법
- Asterisk(*) 기호를 사용하여 함수의 parameter를 표시함
- 입력된 값은 tuple type으로 사용할 수 있음
- 오직 한 개만 맨 마지막 parameter 위치에 사용 가능
- 일반적으로 *args를 변수명으로 사용
- 기존 parameter 이후에 나오는 값을 tuple로 저장함

    def asterisk_test(a, b, *args):
    		return a+b+sum(args)
    
    print(asterisk_test(1, 2, 3, 4, 5))

**Keyword variable-length**

- Parameter 이름을 따로 지정하지 않고 입력하는 방법
- Asterisk(*) 두개를 사용하여 함수의 parameter를 표시한다.
- 입력된 값은 dict type으로 사용할 수 있다.
- 가변인자는 오직 한 개만 기존 가변인자 다음에 사용