---
layout: post
current: post
cover:  assets/images/lab7_17.png
navigation: True
title: Open Source Software - Lab mission 7 - LINUX Web Hosting Service Setup
date: 2018-05-06 02:40:00
tags: [linux]
class: post-template
subclass: 'post tag-getting-started'
author: ykss
---

# Open Source Software - Lab mission 7 - LINUX Web Hosting Service Setup



#### 1.  APT란 무엇인가?

##### Package Tool - APT(Advanced Package Tool) 

Debian 계열의 리눅스에서 사용(Ubuntu)

필요한 패키지를 설치 하거나 업데이트하고 삭제하는 패키지 매니저이다. 



------



#### 2. apt 명령어 정리

*apt-get [option]

	* option : update, install, upgrade, autoremove, remove, purge

> 1) update : 패키지 인덱스 정보를 업데이트
>
> ```
> $ apt-get update
> ```

​	apt-get이 가지고 있는 인덱스 정보 (etc/apt/source.list)를 통해서 패키지 정보를 얻습니다.

> 2) install : 패키지 설치 
>
> ```
> $ apt-get install 패키지명
> ```

> 3) upgrade : 설치된 패키지 업그레이드
>
> ```
> $ apt-get upgrade
> ```

​	설치되어 있는 패키지를 모두 최신 버전을 업그레이드 합니다.

 	*의존성을 갖추기 위해 패키지 추가/삭제도 개의치 않으면 아래 명령어 사용*

```
$ apt-get dist-upgrage
```

> 4) autoremove : 사용하지 않는 패키지 삭제
>
> ```
> $ apt-get autoremove
> ```

> 5) remove : 설정파일을 보존하고 패키지 삭제
>
> ```
> $ apt-get remove 패키지명
> ```

> 6) purge : 패키지와 함께 설정파일 까지 삭제
>
> ```
> $ apt-get purge 패키지명
> ```



*apt-cache [option]

	* option : stats, pkgnames, search, show

> 1) stats :  캐시 현황 확인
>
> ```
> $ apt-cache stats
> ```

> 2) pkgnames : 사용할 수 있는 모든 패키지 출력
>
> ```
> $ apt-cache pkgnames
> ```

> 3) search : 패키지 검색
>
> ```
> $ apt-cache search 패키지명
> ```

​	검색어와 연관된 패키지 이름과 설명 출력

> 4) show : 패키지 정보 보기
>
> ```
> $ apt-cache show 패키지명
> ```



------



#### 3. APM이란 무엇인가?

APM은 Apache2, PHP, MySQL의 앞글자를 따서 만든 단어로

세가지 프로그램을 조합함을 통해서 손쉽게 웹서버를 구축할 수 있다.

세 프로그램 모두 오픈 소스 프로그램이다.



1) Apache2

​	아파치는 웹서버 프로그램으로 오픈 소스 개발방식이며 무료인 프로그램으로 빠른 속도와 

​	안정성을 자랑한다.



2) PHP

​	PHP는 서버 스크립트 언어로, 서버에서 실행되고 해석되는 스크립트 언어다. 다른 언어와 

​	달리 일반적인 html 문서안에서도 사용할 수 있고, DB와 연동이 매우 간편하다. 그리고 

​	UNIX와 WINDOWS 환경 모두에서 작동 가능하다. 문법은 Perl, C와 비슷하며 class를 

​	지원하기 때문에 효율적인 코딩이 가능하다.



3) MySQL

​	공개된 관계형 데이터베이스(RDBMS) 이다. PHP와 연결이 용이하고 공개용 웹서버와 연결이

​	간편하다. 다른 데이터 베이스에 비하여 보안이나, 각종 함수가 잘 갖춰져있다.



------



#### 4.PHP7 설치 정보를 웹으로 확인

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

​	

------



#### 5. MYSQL 설치후 mysqld시작 확인

MySQL을 성공적으로 설치 한 후에, 터미널에 아래와 같이 입력하면 현재 상태확인이 가능하다.

```
$ service mysql status
```

![lab7_1](/assets/images/lab7_1.png)

뿐만 아니라 아래와 같은 명령어를 통해 MySQL 시작/종료/재시작이 가능하다.

```
$ service mysql start
$ service mysql stop
$ service mysql restart
```



------



#### 6. phpmyadmin 설치

phpMyAdmin은 MySQL DB를 관리할 수 있는 웹 인터페이스이다. 다음과 같은 커맨드로

설치가능하다. 아래와 같이 apache2를 서버로 선택하면 된다. phpmyadmin을 통해

웹기반으로 DB를 관리할 수 있다.

```
$ sudo apt-get install phpmyadmin
```

![lab7_2](/assets/images/lab7_2.png)



------



#### 7. apache 서버 시작/중지/재시작

아래와 같은 명령어를 통해 apache 서버를 시작/중지/재시작/상태확인을 할 수 있다.

```
$ service apache2 start
$ service apache2 stop
$ service apache2 restart
$ service apache2 status
```



------



#### 8. 홈 디렉토리 변경

기본 홈 디렉토리는 /var/www/html 로 지정되어있다. 홈디렉토리를 var/www/html2로 바꾸기 

위해서는 홈디렉토리 설정을 변경 해 주어야한다. 

```
$ sudo nano /etc/apache2/sites-available/000-default.conf
```

위와 같은 커맨드를 입력하면 아래와 같이 000-default.conf 파일의 수정화면이 나오는데,

아래서 DocumentRoot 를 var/www/html2과 같이 수정하면 된다. (vi,nano,vim 모두 상관 없다.)

![lab7_3](/assets/images/lab7_3.png)



뿐만 아니라 아래의 apache2.conf 파일 또한 아래 사진과 같이 수정해야한다.

```
$ sudo vi /etc/apache2/apache2.conf
```

![lab7_4](/assets/images/lab7_4.png)



설정파일을 변경하고 저장한 뒤에는 apache2 웹 서버를 재시작 해주어야 적용된다.

```
$ sudo service apache2 restart
```

그냥 html2 폴더를 만들게 되면 권한 문제 (permission denied)가 생길 수 있기 때문에, 아래와 같이

html 폴더를 통째로 복사하면 권한 까지 함께 복사되어 문제를 해결할 수 있다.

```
$ sudo cp -r html html2
```

홈디렉토리 변경 결과, localhost에 접속하면  var/www/html2/index.html 이 화면에 표시된다.

![lab7_5](/assets/images/lab7_5.png)



------



#### 9. SSH server 설치

```
$ apt-get install openssh-server
```

위와 같은 커맨드를 통해 ssh-server를 설치 할 수 있고 ssh-client 같은 경우, 우분투에 기본적으로 설치 되어 있다. 

![lab7_6](/assets/images/lab7_6.png)



```
$ dpkg -l | grep openssh
```

위와 같은 커맨드를 통해 ssh server check가 가능하다. 

![lab7_7](/assets/images/lab7_7.png)



```
$ ifconfig
```

ifconfig 커맨드를 통해 ip 정보를 확인해야 한다. 

![lab7_8](/assets/images/lab7_8.png)

그리고 putty를 실행하여 ip 주소를 입력하는 칸에 ifconfig를 통해 얻은 ip 주소를 입력하면 된다.

![lab7_9](/assets/images/lab7_9.png)

그럼 아래와 같이 ssh 서버에 접속이 된다.

![lab7_10](/assets/images/lab7_10.png)



------

#### 10. 웹 호스팅 virtual host 세팅 

> 사용자 1계정 (ykssss.com)

먼저 유저 계정을 생성하고 패스워드를 설정한다.

 ```
$ useradd -m ykss.com
$ passwd ykss.com
 ```

![lab7_13](/assets/images/lab7_13.png)



사이트 확인을 위해서 새로 만든 디렉토리에 index.html 파일을 생성한다.

![lab7_12](/assets/images/lab7_12.png)



그리고 /etc/apache2/sites-available  경로에 가상호스트 설정 파일이 필요한데,

기존에 있는 000-default.conf 파일을 복사한다. 그리고 아래와 같이 수정한다.

```
$  cp 000-default.conf ykss.com.conf 

ServerName ykss.com
ServerAlias www.ykss.com
ServerAdmin admin@ykss.com
DocumentRoot /home/ykss.com/www
ErrorLog /home/ykss.com/logs/error.log
CustomLog /home/ykss.com/logs/access.log combined
```

![lab7_14](/assets/images/lab7_14.png)

그리고 완성한 설정파일을 sites-enable로 링크해주어야한다.

````
$ a2ensite /etc/apache2/sites-available/ykss.com
````



그리고 /etc/apache2/apache2.conf  의 아파치 설정 파일에 가상호스팅을 추가해야한다.

코드에 아래와 같은 코드를 추가한다.

 <Directory /home/ykss.com/www/>

​        **Options Indexes FollowSymLinks**

​        **AllowOverride None**

​        **Require all granted**

**</Directory>**



*실제 도메인이 존재하지 않기 때문에 강제로 호스트를 지정하는 방법이 필요하다. 

/etc/hosts 파일을 수정하여 

<ip주소> <domain이름> 을 추가해주면 호스트를 지정해줄수 있다. 



저장한 후 아파치를 실행한 후 재시작 하면 아래와 같이 접속한 화면을 볼 수 있다.


````
$ service apache2 restart
````


![lab7_15](/assets/images/lab7_15.png)




>  사용자 2 계정(yksoss.com)

사용자 1계정의 순서와 동일하게 진행되고, 결과 화면은 아래와 같다.

![lab7_16](/assets/images/lab7_16.png)







> 참고 출처
>
> https://blog.outsider.ne.kr/346
>
> http://umax7.netcci.net/bbs/zboard.php?id=study&page=3&sn1=&divpage=1&sn=off&ss=on&sc=on&select_arrange=name&desc=desc&no=26
>
> https://zetawiki.com/wiki/%EB%A6%AC%EB%88%85%EC%8A%A4_MySQL_%EC%8B%9C%EC%9E%91,_%EC%A0%95%EC%A7%80,_%EC%9E%AC%EC%8B%9C%EC%9E%91,_%EC%83%81%ED%83%9C%ED%99%95%EC%9D%B8
>
> http://programmingskills.net/archives/315
>
> http://webdir.tistory.com/213
>
> http://cocoalab.tistory.com/71
>
> http://aeac.tistory.com/23





