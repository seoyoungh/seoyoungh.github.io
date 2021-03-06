---
title:  "웹사이트 배포하기"
excerpt: "Django Girls Tutorial - 나만의 블로그 만들기 2"
toc: true
toc_sticky: true

categories:
  - django
tags:
  - django-girls
  - django
  - web
---
아래 내용은 [Django Girls Tutorial](https://tutorial.djangogirls.org/ko)을 바탕으로 합니다.

### 배포란?
배포(deployment)는 애플리케이션을 인터넷에 올려놓아 다른 사람들도 볼 수 있게 해주는 것 말한다. 이 튜토리얼에서는 `PythonAnywhere`을 사용해 배포했다.

### Github에서 PythonAnywhere로!
로컬 저장소와 GitHub 저장소 연동을 완료했으면, GitHub에 있는 코드를 끌어와 저장소를 clone해 PythonAnywhere로 탑재할 수 있다.

`$ git clone https://github.com/<your-github-username>/my-first-blog.git`

### PythonAnywhere에서 데이터베이스 생성하기
컴퓨터와 서버는 다른 데이터베이스를 사용하므로, PythonAnywhere에서 데이터베이스를 새로 설정해주어야 한다. 방법은 local에서 했던 것과 같다.

### WSGI 프로토콜
장고는 WSGI 프로토콜을 사용해 작동한다. 이 프로토콜은 파이썬을 이용한 웹사이트를 서비스하기 위한 표준이다. WSGI 설정 파일을 수정해 우리가 만든 장고 블로그를 PythonAnywhere에서 인식하게 해주어야 한다. 이 파일은 PythonAnywhere에게 웹 애플리케이션의 위치와 Django 설정 파일명을 알려주는 역할을 한다.

### 웹 개발 공통 작업 과정
Local 에서 GitHub으로, Github에서 PythonAnywhere로! 이 것이 바로 공통적인 웹 개발의 작업 과정이다. 로컬에서 변경하고, 변경 사항을 GitHub에 적용하고, 변경 사항을 실제 웹 서버로 가져 온다. 이를 통해 실제 웹 사이트를 손상시키지 않고 작업하고 테스트 해볼 수 있다. 내가 블로그 글을 작성한 로컬에서 테스트하고, GitHub에 push해 서버에 적용시키는 메커니즘과 같다.
