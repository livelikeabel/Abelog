---
title: List Data Type
date: 2019-09-13 23:09:33
category: python
---

# List Data Type

*python에는 Array가 따로 존재한다.*

### **LIST**

- 시퀀스(순서대로) 자료형, 여러 데이터들의 집합
- 인덱싱
    - list에 있는 값들은 주소(offset)을 가진다.
- 슬라이싱
    - list의 값들을 잘라서 쓰는 것이 슬라이싱
    - list의 주소 값을 기반으로 부분 값을 반환

        cities = ['서울', '부산', '인천', '대구', '대전', '광주', '울산', '수원']
        print(cities[0:6], a[-9:]) # a 변수의 0부터 5까지, -9뿌터 끝까지
        print(cities[:]) # a변수의 처음부터 끝까지
        print(cities[-50:50]) # 범위를 넘어갈 경우 자동으로 최대 범위를 지정
        print(cities[::2], a[::-1]) # 2칸 단위로, 역으로 슬라이싱
        
        # ( start : end : step )

- **리스트의 연산**

    인덱싱, 슬라이싱, 연산 등 활용

        color = ['red', 'blue', 'green']
        color2 = ['orange', 'black', 'white']
        
        color + color2
        # >>> ['red', 'blue', 'green', 'orange', 'black', 'white']
        # 대용량 데이터일 때는 메모리를 많이 잡아먹기 때문에 좋은 방법은 아니다.
        
        len(color)
        # >>> 3 (리스트의 길이)
        
        color[0] = 'yellow'
        # >>> ['yellow', 'blue', 'green'] 0번째 리스트의 값을 변경
        
        color * 2
        # >>> ['yellow', 'blue', 'green', 'yellow', 'blue', 'green']
        
        "red" in color
        # >>> False

- **리스트의 추가와 삭제**

    append, extend, insert, remove, del 등 활용

        color = ['yellow', 'blue', 'green']
        color2 = ['orange', 'black', 'white']
        
        color.append("red")
        # >>> ['yellow', 'blue', 'green', 'red']
        
        color.extend(color2)
        # >>> ['yellow', 'blue', 'green', 'red', 'orange', 'black', 'white']
        
        color.insert(0, "abel")
        # >>> ['abel', 'yellow', 'blue', 'green', 'red', 'orange', 'black', 'white']
        
        del color[0]
        # >>> ['yellow', 'blue', 'green', 'red', 'orange', 'black', 'white']
        
        color.remove("red")
        # >>> ['yellow', 'blue', 'green', 'orange', 'black', 'white']

    append와 extend는 값 자체가 변하는 것이다.

### python 리스트만의 특징

- 다양한 Data type이 하나에 List에 들어갈 수 있다. (Dynamic typing - 변수의 타입이 실행시점에 결정된다.)

    *tip: is로 주소값을 비교할 수 있다. == 은 값비교.*

### 패킹과 언패킹

- 패킹: 한 변수에 여러 개의 데이터를 넣는 것.
- 언패킹: 한 변수의 데이터를 각각의 변수로 변환.

    >>> t = [1, 2, 3]  # 1,2,3을 변수 t에 패킹
    
    >>> a, b, c = t    # t에 있는 값 1, 2, 3 을 변수 a, b ,c에 언패킹

### 이차원 리스트

- 리스트 안에 리스트를 만들어 행렬(Matrix)생성

    >>> kor_score = [49,79,20,100,80]
    >>> math_score = [43,59,85,30,90]
    >>> eng_score = [49,79,,48,60,100]
    >>> midterm_score = [kor_score, math_score, eng_score]
    >>> print(midterm_score[0][2])
    # 20


출처: https://www.inflearn.com/course/python-파이썬-입문-강좌