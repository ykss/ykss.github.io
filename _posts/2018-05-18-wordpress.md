---
layout: post
current: post
cover:  assets/images/basic.png
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