---
layout: post
current: post
cover:  assets/images/writing.jpg
navigation: True
title: Open Source Software - Lab mission 8 - Parse Json File
date: 2018-05-24 22:00:00
tags: [linux]
class: post-template
subclass: 'post tag-getting-started'
author: ykss
---

# Parse Json File 

## 1. Read & Append String 

* Console input - read_string_from_console() 구현

 빈 문자열을 입력할 때 까지 반복문을 돌리고, 키보드로부터 입력받은 문자열을 이어붙인 문자열을 만든다. (리턴값은 이어붙인 전체 문자열이다.)

![lab8_6](/assets/images/lab8_6.png)

위와 같은 코드를 컴파일 시키고 실행 시키면 아래와같은 결과가 나온다.

![lab8_7](/assets/images/lab8_7.png)


* File input - read_string_from_file(char filename[]) 구현

 텍스트파일을 열러 한줄씩 읽으면서 이를 하나의 문자열로 이어붙인다.

다음은 코드이다.

![lab8_10](/assets/images/lab8_10.png)

data.txt파일의 내용은 아래와 같다.

![lab8_8](/assets/images/lab8_8.png)

실행결과는 아래와 같다.

![lab8_9](/assets/images/lab8_9.png)


## 2. JSMN reload
: 기존에 정해진 스트링 대로 읽어왔던 방식이 아닌 json 텍스트를 읽는 방식이다. - char * readjsonfile()

위에서 만든 read_string_from_file()를 활용하여 
readjsonfile()를 만들 수 있다.

![lab8_16](/assets/images/lab8_16.png)

data.json의 내용은 아래와 같다.

![lab8_11](/assets/images/lab8_11.png)

MAKEFILE을 수정하여 컴파일하도록 한다.

![lab8_12](/assets/images/lab8_12.png)
![lab8_15](/assets/images/lab8_15.png)

make 명령어를 통해 실행파일을 생성한다.

![lab8_13](/assets/images/lab8_13.png)

아래가 실행한 파일로 json파일을 파싱한 결과이다. 

![lab8_14](/assets/images/lab8_14.png)


