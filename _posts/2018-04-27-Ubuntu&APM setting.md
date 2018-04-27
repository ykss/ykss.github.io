---
layout: post
current: post
cover:  assets/images/lab6_7.png
navigation: True
title: Open Source Software - Lab mission 6 - 나만의 웹서비스 환경구축
date: 2018-04-27 19:50:00
tags: [linux]
class: post-template
subclass: 'post tag-getting-started'
author: ykss
---

# Lab quest 6 - 나만의 웹서비스 환경구축 



## 1. vmware 설치

https://www.vmware.com/kr/products/workstation-player/workstation-player-evaluation.html

위의 주소에 접속하면 다음과 같은 화면을 볼 수 있다.

![lab6_1](/assets/images/lab6_1.png)

아래의 화면에서 Windows용 Workstation 다운로드를 클릭한다. 그리고

설치파일을 실행하고 설치 과정에 따라 설치를 완료한다.



## 2.ubuntu 설치

우분투 홈페이지 (https://www.ubuntu.com/download/desktop ) 에 접속하면 

우분투를 다운받을 수 있다. 다운로드 버튼을 누르면 기부를 할 수 있는 메뉴가 나오는데

아래 쪽에 "Not now, take me to the download" 버튼을 누르면 이 단계를 스킵하고 ubuntu를 다운 받을 수 있다. 

![lab6_2](/assets/images/lab6_2.png)

그리고 아까 설치했던 vmware을 실행하면 다음과 같은 화면이 뜬다.

![lab6_3](/assets/images/lab6_3.png)

위의 메뉴 중 Create a New Virtual Machine 메뉴를 클릭하면 새로운 가상머신을 만드는 메뉴가 나온다.

다음 메뉴 중 가운데 옵션을 선택하고 아까 다운받은 ubuntu.iso파일을 찾아 선택한다.

![lab6_4](/assets/images/lab6_4.png)

그리고 가상머신 이름과 계정정보 설정을 한다.

![lab6_5](/assets/images/lab6_5.png)

가상머신에 대한 설정을 변경할 수 있다.

![lab6_6](/assets/images/lab6_6.png)

가상머신 생성 완료 후 실행되면 다음과 같은 화면이 나오고 설치가 진행되며, 설치가 완료되면 초기화면이 뜬다.

![lab6_7](/assets/images/lab6_7.png)

![lab6_8](/assets/images/lab6_8.png)

![lab6_9](/assets/images/lab6_9.png)

우분투의 설치가 완료되었다.



## 3. APM(Apache & PHP & MySQL) 설치

ubuntu 에서 `ctrl+alt+t`를 입력하면 다음과 같은 터미널이 뜬다. 

모든 설치 과정은 터미널을 통해 진행된다. 

![lab6_10](/assets/images/lab6_10.png)

패키지 설치 전 저장소의 패키지 목록을 업데이트하고, 기존 설치되있던 패키지를 

업그레이드 해야한다.

```
$ sudo apt-get update
$ sudo apt-get upgrade
```

![lab6_11](/assets/images/lab6_11.png)

> Apache2 web server 설치

```
$ sudo apt-get install apache2
```

위의 커맨드를 입력하면 아래와 같이 설치된다.

![lab6_12](/assets/images/lab6_12.png)

웹브라우저를 실행하고 localhost에 접속하여 아래 결과화면을 보면 성공적으로 설치된것이다.

![lab6_13](/assets/images/lab6_13.png)



> MySQL 서버 설치

```
$ sudo apt-get install mysql-server
```

커맨드를 입력하면 아래와 같이 설치된다.

![lab6_14](/assets/images/lab6_14.png)

> PHP 설치

 PHP 패키지 다운을 위한 저장소 추가

```
$ sudo add-apt-repository ppa:ondrej/php
```

추가한 저장소에서 패키지 목록을 업데이트

```
$ sudo apt-get update
```

PHP설치 커맨드

```
$ sudo apt-get install php7.2 php7.2-common
```

PHP 7.2 추가 패키지 설치

```
$ sudo apt-get install php7.2-mysql php7.2-curl php7.2-xml php7.2-zip php7.2-gd php7.2-mbstring
```

![lab6_15](/assets/images/lab6_15.png)

아래와 같은 커맨드를 통해 PHP가 제대로 설치되었는지 확인한다.

```
$ sudo sh -c 'echo "<?php phpinfo(); ?>" > /var/www/html/info.php'
```

웹브라우저에 localhost/info.php로 접속해 아래와 같은 화면이 나오면 정상적으로 설치된것이다.

![lab6_16](/assets/images/lab6_16.png)

또한 `$ php -v `와 같은 커맨드를 통해 버전 확인이 가능해야한다.



> phpMyAdmin 설치

phpMyAdmin은 MySQL DB를 관리할 수 있는 웹 인터페이스이다. 다음과 같은 커맨드로

설치가능하다. 아래와 같이 apache2를 서버로 선택하면 된다. phpmyadmin을 통해

웹기반으로 DB를 관리할 수 있다.

```
$ sudo apt-get install phpmyadmin
```

![lab6_17](/assets/images/lab6_17.png)

> git 설치

다음과 같은 명령으로 git 을 설치할 수 있다.

```
$ sudo apt-get install git
```



# #4.index.html 수정해보기

/var/www/html/index.html 파일을 수정하면 localhost/index.html의 초기화면을 수정할 수 있다.

![lab6_18](/assets/images/lab6_18.png)

파일의 내용을 수정하면 아래와 같이 localhost에 접속했을때 수정한 내용이 표시된다.

![lab6_19](/assets/images/lab6_19.png)





> 참고출처) http://recipes4dev.tistory.com/111
>
> ​		http://webnautes.tistory.com/1028