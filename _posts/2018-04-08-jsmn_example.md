---
layout: post
current: post
cover:  assets/images/lab4_3.png
navigation: True
title: Open Source Software - Lab mission 4 - jsmn example code analysis
date: 2018-04-08 23:45:00
tags: [jsmn]
class: post-template
subclass: 'post tag-getting-started'
author: ykss
---

# JSMN Example Analysis


### 분석대상 파일 : simple.c, jsondump.c



### 1. 각 소스의 흐름과 변수 의미, 용도 

#### `simple.c`

> simple_example의 실행 결과


![lab4_1](/assets/images/lab4_1.png)


실행결과를 보았을 때,  JSON 형식의 데이터를 파싱하여 위와 같은 형식으로 출력해주는 것이다.

JSON_STRING 이라는 Char 형 변수에 JSON 형식으로 아래와 같이 정의되어있는데,

아래의 데이터를 바탕으로 , 한 눈에 파악하기 쉬운 형식으로 출력해준다.

```
static const char *JSON_STRING =
	"{\"user\": \"johndoe\", \"admin\": false, \"uid\": 1000,\n  "
	"\"groups\": [\"users\", \"wheel\", \"audio\", \"video\"]}";
```

출력 결과를 바탕으로 소스를 분석했을 때, 먼저 파서를 만들고 파서를 통해 JSON_STRING에 저장되어있는 데이터를 파싱하여 Object, string, primitive type등 으로 나눈다. 그리고 토큰의 개수인 r값이 음수가 나오면 파싱 실패에러를 표시하고, 첫번째 토큰에는 object타입이 오게한다. 그 이후에 for문을 통해 토큰 하나하나의 저장되어있는 값을 분석한다.  이때 jsoneq()함수를 호출하여 파싱을 진행하는데,  jsoneq함수는 예시 데이터인 JSON _STRING과 토큰값인 t[i], 그리고 파싱할 데이터의 attribute 스트링을 파라미터로 하여 만약 토큰의 타입이 스트링과 같고, 길이가 같고 비교한 스트링의 내용이 같으면 0을 리턴하고 그렇지 않을 경우 -1을 리턴한다. 그래서 0을 리턴했을 때만, 형식에 맞추어 출력해주고 i값을 증가 시켜 다음 토큰을 검사한다. 그래서 user, admin 등 차례대로 검사하다가 groups는 array 타입이기 때문에 변수 j를 만들어 for을 중첩하여 배열의 인덱스 별로 parsing한다. 그리고 위에서 정해진 arribute가 나온다면 unexpected key로 분류하여 출력한다.



#### `jsondump.c`

> jsondump.c의 실행결과

![lab4_4](/assets/images/lab4_4.png)

실행결과를 보면 먼저 프로그램을 실행하면 입력을 기다린다. 그리고 JSON 데이터 형식에 맞게 {user: johndoe, admin: false, uid: 1000, groups: [users, wheel, audio, video] } 와 같은 값을 입력 후 EOF를 입력하면 simple_example의 실행결과와 비슷한 형식으로 출력해준다. `simple.c`와 다른 것은 `simple.c`에서는 예시 스트링데이터를 미리 정의하여 제공하였다면,` jsondump.c`에서는 사용자로 부터 제공받은 데이터를 파싱하여 나타낸다는 것이다.  그렇기 때문에 메모리 할당이 가장 큰 차이점이라고 할 수 있겠다. 

```
static inline void *realloc_it(void *ptrmem, size_t size) {
	void *p = realloc(ptrmem, size);
	if (!p)  {
		free (ptrmem);
		fprintf(stderr, "realloc(): errno=%d\n", errno);
	}
	return p;
}
```

위 의 함수는 `jsondump.c` 에서 핵심적인 기능을 하는 함수이다. 언뜻보면 일반적인 realloc()과 다를게 없어 보이지만, 하나의 차이점이 있다. 그것은 realloc()이 실패할 경우 이전의 메모리 포인터의 할당을 해제한다.  따라서 realloc_ it ()을 호출한 후에는 이전의 메모리 포인터는 사용할 수 없다.큰 흐름을 보면 main함수에서 먼저 토큰에 malloc()을 통해 메모리 할당을 해주고 `for (;;)` 를 통해 무한 루프를 열어 fread()를 통해 사용자로 부터 데이터를 입력받는다. 그리고 입력받고나서 그만큼 realloc_ it()을 통하여 메모리를 재할당한다. 그리고 jsmn_parse()함수를 통해 토큰에다 파싱을 하고 만약 파싱의 리턴값이 0보다 작다면 메모리를 더 크게 재할당 해준다. 그리고 다시 파싱을 진행한다. 문제없이 파싱이 끝난다면 dump()함수를 호출하고, dump()함수는 파싱한 결과를 바탕으로 결과값을 형식에 맞게 출력한다.



### 2. 각 소스에서 jsmn 라이브러리를 사용하는 순서 



#### `simple.c`


1) `jsmn_parser p;` : main함수에서 jsmn_parser 타입의 변수 p를 선언

2) `jsmntok_t t[128];`  : jsmntok_t 타입의 배열 변수 t[128] 선언. 토큰이 저장되는 곳.

3) ` jsmn_init(&p); `: jsmn_init 함수를 p의 주소값을 파라미터로 호출하여 사용가능한 토큰 배열을 
​    사용하여 제공된 버퍼를 기반으로 new JSON parser를 만들고 파서를 초기화한다.

4) `r = jsmn_parse(&p, JSON_STRING, strlen(JSON_STRING), t, sizeof(t)/sizeof(t[0]));`
​    : jsmn_ parse함수를 호출하여 JSON parser를 실행한다. 호출할 때 , p의 주소값과 예시 데이터가 ​      들어있는 JSON_STRING과 그 배열의 길이, 그리고 저장할 토큰 배열등이 파라미터로 전달된다. 그리고 리턴 값인 저장된 토큰의 개수가 r에 저장된다.  그리고 각 토큰에 데이터 타입에 맞게 파싱된 데이터가 저장된다. 

5) `jsmntok_t *g = &t[i+j+2];`  : array 타입 저장 시 jsmntok_t 타입의 토큰 변수 g를 하나 만들어 따로 저장한다.



#### `jsondump.c`


1)`jsmn_parser p;` : parser 타입의 변수 p 선언.

2)`jsmntok_t *tok;` : token 생성

3) `jsmn_init(&p);` : jsmn_init 함수를 p의 주소값을 파라미터로 호출하여 사용가능한 토큰 배열을 사용하여 제공된 버퍼를 기반으로 new JSON parser를 만들고 파서를 초기화한다.

4) `r = jsmn_parse(&p, js, jslen, tok, tokcount);` :  여러가지 파라미터를 보내 파싱하고 r에는 ​    저장된 토큰의 개수가 저장된다. 그리고 r<0이고 에러가 나면 토큰개수를 두배로 늘리고 메모리를 재할당 한다. 그리고 goto문을 통해 다시 jsmn_parse()를 호출한다. 그리고 r>=0이면 dump() 함수를 호출한다.



### 3. 각 예제에 JSON 텍스트를 다른 내용으로 적용 

#### `simple.c`

![lab4_2](/assets/images/lab4_2.png)

#### `jsondump.c`

![lab4_3](/assets/images/lab4_3.png)







