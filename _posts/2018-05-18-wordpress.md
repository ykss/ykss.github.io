---
layout: post
current: post
cover:  assets/images/lab8_2.png
navigation: True
title: Open Source Software - Lab mission 8 - Wordpress setup in ubuntu
date: 2018-05-18 22:00:00
tags: [linux]
class: post-template
subclass: 'post tag-getting-started'
author: ykss
---

#우분투에 워드프레스 설치하기

1. 먼저 워드프레스를 설치할 계정을 새로 추가한다.
```
$ sudo useradd -m <username>
```
내 경우에는 -m을 붙여주지 않으면 /home 디렉토리에 새로운 유저의
기본 폴더가 생성되지 않아서 붙여줬다.
`passwd` 명령어로 유저의 비밀번호 설정이 가능하다.

2. 워드프레스 다운로드
```
 $ cd /home/wpuser/www
 $ wget http://ko.wordpress.org/wordpress-3.6-ko_KR.tar.gz
 $ tar -xvzf wordpress-3.6-ko_KR.tar.gz
```
위의 커맨드와 같이 생성한 유저 폴더에 워드프레스를 다운받고 압축을 해제한다.

3. mysql에 데이터베이스 준비
```
$ mysql -u root -p
mysql> create database wordpress;
mysql> create user 'root'@'localhost'identify by '암호';
mysql> grant all on wpdb.* to 'root'@'localhost';
mysql> flush previleges;
```

4. wp.config파일 준비

![lab8_2](/assets/images/lab8_2.png)

위와 같은 화면이 뜬다면 워드프레스가 성공적으로 설치된 것이다.

![lab8_1](/assets/images/lab8_1.png)

위와 같이 DB이름, 유저이름, 비밀번호, 호스트서버를 입력하고
저장하면, wp.config 파일의 준비가 완료된다.

또는, 웹상에서 설정도 가능하다.
설정을 성공적으로 마치면 wp.config 파일이 생성된다.

5. 워드프레스 작동 확인

localhost/wordpress 에 접속하게 되면 아래와 같이 
로그인 화면이 뜬다.

![lab8_4](/assets/images/lab8_4.png)

설정한 아이디와 비밀번호로 접속에 성공하면 바르게 작동하는 것이다.

![lab8_5](/assets/images/lab8_5.png)