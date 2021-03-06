---
title:  "Web 기초 & Django란?"
excerpt: "Django Girls Tutorial - Web은 무엇이며 Django는 또 뭐지?"
toc: true
toc_sticky: true

categories:
  - django
tags:
  - django-girls
  - django
  - web
---

장고를 배워보기로 결심하고, 개발팀 인턴 분이 추천해준 장고걸스 튜토리얼로 시작하기로 했다! 해당 튜토리얼을 시작하기 전에, 기본적으로 웹에 대해 복습하기 위해 [생활코딩 Web 강좌](https://opentutorials.org/course/3084), [생활코딩 서버 강좌](https://opentutorials.org/course/669)를 참고했다.

아래 내용은 [Django Girls Tutorial](https://tutorial.djangogirls.org/ko)을 바탕으로 합니다.

## Web 간단 정리!
- **Client & Server**: 클라이언트는 서버에 request, 서버는 이에 response한다. 웹은 클라이언트인 웹브라우저와 서버인 웹서버로 이루어진다. 웹브라우저에 url을 입력하면, 그 url로 해당하는 웹서버에 웹페이지에 대한 요청이 전달되는 것이다. 그리고 웹서버는 웹브라우저가 요청한 정보를 제공한다.
- **PHP**: 서버 측에서 실행되는 프로그래밍 언어이다. HTML을 프로그래밍적으로 생성해주고, 데이터베이스와 상호작용 하면서 데이터를 저장하고, 표현한다. Django는 Python을 사용한다.
- **HTML**: 웹페이지를 만드는 코드
- **IP**: 인터넷에 연결되어 있는 장치(컴퓨터, 스마트폰, 서버 등등)들은 각각의 장치를 식별할 수 있는 주소를 가지고 있는데 이를 ip라고 한다. e.g.) 115.68.24.88, 192.168.0.1
- **DNS(Domain Name System)**: IP주소는 불편하기 때문에, 각 IP에 이름을 부여한 것이 도메인이다. e.g.) naver.com, github.com
- cf) 도메인의 IP 주소가 궁금하다면 커맨드 창에서 nslookup naver.com과 같이 입력하면 IP 주소를 알 수 있다!
- **URL**: 도메인 + 경로 e.g.) github.com/blahblah
- **네트워크**: 두 대 이상의 컴퓨터들을 마치 그물망처럼 연결해 서로 통신할 수 있게 해주는 것이다. LAN, WAN 등과 같은 네트워크가 있다. 컴퓨터가 아닌 하드웨어를 연결하는 것도 네트워크이므로, 전화도 네트워크에 해당한다.
- **HTTP(Hypertext Transfer Protocol)**: 인터넷에서 데이터를 주고받을 수 있는 프로토콜. 프로토콜은 규칙으로, 웹 상에서 일어나는 요청과 응답에 대한 규칙이라고 보면 될 것 같다. 이 프로토콜을 통해 서버와 클라이언트 간 정보 교환이 가능하다.
- **포트(Port)**: 포트는 말 그대로 항구다. IP 주소 뒤에 `:4000`과 같이 붙는 것이 포트 번호이다. 컴퓨터에선 여러 개의 프로그램이 동시에 실행되므로, 어떤 프로그램이 내가 접속하여는 프로그램인지 컴퓨터에게 알려주어야 한다. 이 때 포트번호는 어떤 프로그램에 접속할 것인지 컴퓨터에게 알려준다.  
- **데이터 패킷**: 통신망을 통해 전송하기 쉽도록 자른 데이터의 전송 단위, 장고걸스 튜토리얼에서는 많은 양의 편지라고 표현한다.
- **라우터**: 공유기다. 패킷이 여러 개의 편지였다면, 라우터는 각기 다른 우체국이다. 서로 다른 네트워크를 연결해주기 위해서 사용되는 인터넷 접속 장비이다. 패킷의 위치를 추출하여 그 위치에 대한 최상의 경로를 지정하고, 이 경로를 따라 데이터 패킷을 다음 장치로 전향시키는 장치이다.

## What is Django?
> 파이썬으로 만들어진 무료 오픈소스 Web Framework이다.

### 그러면 Framework는 뭔데?
* Framework: 소프트웨어의 구체적인 부분에 해당하는 설계와 구현을 재사용이 가능하게끔 일련의 협업화된 형태로 클래스를 제공하는 것
* Library는 자주 사용되는 로직을 재사용 하기 위한 코드들의 집합, 즉 `부품`이고, Framework는 `뼈대`라고 할 수 있다.
* 자바 프레임워크에는 Spring, 자바스크립트 프레임워크에는 AngularJS, React, 프론트엔드 프레임워크에는 Bootstrap 등이 있다.

### Django Framework는 다음과 같이 쉽고 빠르게 웹사이트를 개발할 수 있게 도와준다!
* 회원가입, 로그인, 로그아웃과 같이 사용자 인증을 다루는 방법이나 웹사이트의 관리자 패널, 폼, 파일 업로드와 같은 요소들을 구현해준다.
* 웹 서버에 요청이 오면 장고로 전달된다. 장고 urlresolver는 웹 페이지의 주소를 가져와 무엇을 할지 확인한다.
* 이 urlreslover는 그리 똑똑하지 않다. 패턴 목록을 가져와 URL과 맞는지 처음부터 하나씩 대조해 식별한다. 만약 일치하는 패턴이있으면, 장고는 해당 요청을 관련된 함수(view)에 넘겨준다.
* 모든 재미난 일들은 view 함수에서 처리된다! - 특정 정보를 데이터베이스에서 찾을 수 있다. 그런데 만약 사용자가 데이터를 바꿔달라고 수정을 요청한다면? view함수는 수정할 수 있는 권한이 있는지 확인하고 나서, 수정을 마치고 view는 답장을 생성한다. 장고는 그 답장을 그 사용자의 웹 브라우저에 보내주는 역할을 한다.
