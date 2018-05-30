---
layout: post
current: post
cover:  assets/images/design.jpg
navigation: True
title: Open Source Software - Lab mission 9 - Find keys and value from json
date: 2018-05-30 22:00:00
tags: [linux]
class: post-template
subclass: 'post tag-getting-started'
author: ykss
---

# Find keys and value from json

## 1. Read data from json text file - readjsonfile() 구현

 json 파일로부터 한줄씩 읽어온다.

![lab9_5](/assets/images/lab9_5.png)

 결과는 아래와 같다. 

![lab9_1](/assets/images/lab9_1.png)


## 2. Json token 정보 출력 - printall() 구현

아래와 같은 함수를 통해 json의 모든 토큰 정보를 얻을 수 있다.

![lab9_9](/assets/images/lab9_9.png)

결과는 아래와 같이 번호, 키, 사이즈 등이 나온다.

![lab9_2](/assets/images/lab9_2.png)


## 3. Json keys 출력 - printkeys() 구현

아래와 같은 함수로 json에서 keys에 해당하는 값만 출력할 수 있다.

![lab9_4](/assets/images/lab9_4.png)

아래와 같은 결과가 나온다. 

![lab9_6](/assets/images/lab9_6.png)

## 4. Json key token array 찾기 - findkeys() 구현

아래와 같이 키에 해당하는 토큰의 번호만 keys라는 int형 포인트 배열에 저장하고
그 개수를 반환한다.

![lab9_9](/assets/images/lab9_10.png)

## 5. 키 토큰별로 해당 값을 출력 - printvalues() 구현

key : value 의 형식으로 출력하는 함수이다.

![lab9_8](/assets/images/lab9_8.png)

실행 결과는 아래와 같다.

![lab9_6](/assets/images/lab9_7.png)





