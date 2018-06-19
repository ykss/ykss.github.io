---
layout: post
current: post
cover:  assets/images/flureact.jpg
navigation: True
title: Flutter versus ReactNative
date: 2018-06-19 22:00:00
tags: [tech]
class: post-template
subclass: 'post tag-getting-started'
author: ykss
---
   
# Flutter vs React Native vs Ionic

### 1. Flutter

> Build beautiful native apps in record time

* Architecture
리액트와는 다르게 브릿지가 존재하지 않는다. 대신 Dart와 C++로 만들어진다.
대부분 네이티브 부분에서 이루어지기 때문에 속도가 빠른편이다.

![flutter_architecture](/assets/images/fluarchi.png)

* 장점
1. dart가 c++로 컴파일 되고 이로인해 속도가 매우 빠르다.
2. 크로스플랫폼 솔루션 중 네이티브에 가장 가깝다. 
3. 구글 서비스이기 때문에 여러가지 구글 서비스와 연동이 쉽다. (ex : firebase)
4. 공식사이트에 도큐멘테이션이 더 짜임새 있게 짜여있다.

* 단점
1. 아직은 신기술이기 때문에 React에 비해서는 라이브러리와 리소스가 적은 편이다.
2. Dart라는 언어를 통해 개발하기 때문에 새로운 언어를 학습해야한다.
(그러나 자바와 비슷하여 장벽이 낮다.)
3. 아직 완전한 서비스가 아닌 베타 단계이기 때문에 개발중이다.
4. 32비트 ios는 지원하지 않는다. (아이폰5 단계)

### 2. React Native
: Reactive view Frameworks

> Build native mobile apps using Javascript and React

* Architecture
자바스크립트와 네이티브 두 파트로 나눠져있다. 그래서 중간에 브릿지라는 존재가 필요하다. 브릿지는 자바스크립트로도 네이티브를 가능하게 한 파워풀한 도구이지만 속도를 느리게 만드는 요소이기도 하다. 특히 UI와 애니매이션을 쓸때는 더 느려진다. 

![react_architecture](/assets/images/react.png)

* 장점
1. 라이브러리와 리소스가 매우 많다. 개발자 커뮤니티가 매우 발전해 있다.
2. Javascript 자체가 많이 쓰이는 언어이기 때문에, 조금 더 보편화된 언어 능력을 키울 수 있다.

* 단점
1. 자바스크립트와 네이티브 사이에 변환을 거쳐야하기 때문에 속도가 늦다.

### 3. Ionic (+bonus)
: Webview Frameworks

* 장점 
1. 앵귤러 기반이다
2. 커뮤니티가 매우크다.
3. 생산성이 좋다.(같은 코드로 데스크탑,웹,모바일,PWA 모두 가능)

* 단점 
1. 2015년 출시된 프레임워크이기 때문에, 아직 버그가 많은 편이다.
2. flutter와 비교하면 여전히 느린편.
