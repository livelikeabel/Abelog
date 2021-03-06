---
title: JPEG, PNG, BMP 톺아보기
date: 2019-04-02 23:04:91
category: development
---

### `JPG, PNG, BMP` 들어본적은 있는데, 뭐하는 애들일까...?
> *wiki를 검색해보자*

- `jpg(jpec)`은 <u>정지 화상</u>을 위해서 만들어진 손실 압축 방법의 표준이다.
- `png`는 비손실 <u>그래픽 파일 포맷</u>의 하나이다. 특허 문제가 얽힌 GIF 포맷의 문제를 해결하고 개선하기 위해서 고안되었다.
- `bmp` 파일 포맷은 비트맵 디지털 그림을 저장하는 데 쓰이는 <u>그림파일 포맷</u>이다. 특히 MS의 window운영 체제에 널리 쓰인다.

👉 뭔가 어려운 말이 잔뜩 있지만 simple하게 말하면, 그냥 **`이미지 파일 압축 형식`**이구나.
<br/>
<br/>
> *무엇 때문에 이렇게 다양한 이미지 파일 형식이 생긴걸까?
<br/>각각의 특징, 장점, 단점을 알아보도록 하자!*

### JPEC(JPG)
**✨특징**
- Joint Photographic Experts Group(합동사진전문가단체)에 의해 <u>인터넷에서의 사진(정지 화상)을 위해서 만들어진 **압축 방법** 표준</u>이다.
- `손실 압축기법`을 사용한다.
> 손실 압축기법이란 반복되는 색상의 수를 단계별로 줄여가는 방법이며 높은 압축율을 가질수록 이미지의 손실은 커진다.
- 넓은 범위의 색을 지원한다(16,772,216가지의 색상)
- 파일의 크기가 작다.
- 사용자가 직접 압축률을 지정하여 압축할 수 있는 형식이다.
- RGB신호를 그대로 사용하지 않고, 비디오에서 많이 사용하는 YCbCr방식으로 변환해 처리한다.
<br/>
<br/>

**👍장점**
- 용량대비 화질이 뛰어나다
- 파일의 크기가 **작기** 때문에 **웹**에서 널리 쓰인다.
- 16,772,216 가지의 색상을 표현 할 수 있어 사진과 같은 실사 이미지 표현에 적합하다
- 사용자가 직접 이미지의 질과 크기를 조절 할 수 있다.
- 압축수준 대비 이미지 구현 품질이 어떤 포맷 형식보다도 훌륭하다. 
- 압축률이 가장 뛰어나다.
<br/>
<br/>

**😭단점**
- 문자, 선, 세밀한 격자 등 고주파 성분이 많은 이미지(로고, 마크, 도형, 도표)의 변환에서는 GIF나 PNG에 비해 불리하며, 나쁜 품질을 보이는 경우가 많다.
- `손실 압축기법`을 사용하기에, 화질을 손상시키며 파일을 저장한다.
<br/>
<br/>

**✏️use case**
- 다수의 색상을 사용한 자연 사진 등의 압축시에 사용한다.
<br/>
<br/>

### PNG
**✨특징**
- Portable Network Graphics의 약어
- `무손실 압축`을 사용한다.
  > 무손실 압축: 디지털 원본과 100% 똑같은 형태를 유지하여 압축하는 방식이다.
- 투명 백그라운드를 지원한다.
- 8비트컬러(256색)와 [트루컬러](https://ko.wikipedia.org/wiki/%ED%8A%B8%EB%A3%A8%EC%BB%AC%EB%9F%AC)를 지원한다.(16,777,216개의 색상 사용가능)
<br/>
<br/>

**👍장점**
 - 이미지 디테일 손실이 전혀 없다. JPEG 형식보다 고품질 이미지를 생성한다.
 - 온라인에 게시할 때, 텍스트와 로고를 선명하게 유지한다. 
 - 고화질의 재편집을 해야하는 상황에 유리하다.(`무손실 압축`이기 때문에)
 - 투명한 배경을 사용할 때 유리하다. 
<br/>
<br/>

**😭단점**
- 용량이 크다.
<br/>
<br/>

**✏️use case**
- 로고, 마크, 도형, 도표에 적합하다.(문자나 날카로운 경계가 있는 그림)
<br/>
<br/>

### BMP
**✨특징**
- 윈도우 기반 PC에 널리 사용되는 그래픽 파일의 형식이다.
- `무손실 압축`을 사용한다.
<br/>
<br/>

**👍장점**
- 호환성이 매우 높다.
<br/>
<br/>

**😭단점**
- 이미지 크기에 비해 용량이 매우 크다.
<br/>
<br/>

------------

### 출처

JPEG
- https://ko.wikipedia.org/wiki/JPEG
- http://www.itworld.co.kr/t/62072/%EB%94%94%EF%BF%BD%EF%BF%BD%EF%BF%BD%ED%84%B8%EC%9D%B4%EB%AF%B8%EC%A7%80/98431
- https://m.blog.naver.com/PostView.nhn?blogId=eclick&logNo=110024943034&proxyReferer=https%3A%2F%2Fwww.google.com%2F

PNG
- https://ko.wikipedia.org/wiki/PNG
- http://mwultong.blogspot.com/2006/06/png-png-portable-network-graphics.html

BMP
- https://ko.wikipedia.org/wiki/BMP_%ED%8C%8C%EC%9D%BC_%ED%8F%AC%EB%A7%B7
- http://jinyongjeong.github.io/2016/05/29/image_type/