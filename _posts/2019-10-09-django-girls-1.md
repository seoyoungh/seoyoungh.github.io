---
title:  "Django Girls"
excerpt: "Django로 나만의 웹페이지 만들기"
toc: true
toc_sticky: true

categories:
  - django-girls
tags:
  - django
  - web
---

## Django
* Web Framework
    * 회원가입, 로그인, 로그아웃과 같이 사용자 인증을 다루는 방법이나 웹사이트의 관리자 패널, 폼, 파일 업로드 등을 
    * 웹 서버에 요청이 오면 장고로 전달된다. 장고 urlresolver는 웹 페이지의 주소를 가져와 무엇을 할지 확인합니다.
- 이 urlreslover는 그리 똑똑하지 않습니다. 패턴 목록을 가져와 URL과 맞는지 처음부터 하나씩 대조해 식별합니다. 만약 일치하는 패턴이있으면, 장고는 해당 요청을 관련된 함수(view)에 넘겨줍니다.
- 모든 재미난 일들은 view 함수에서 처리됩니다: 특정 정보를 데이터베이스에서 찾을 수 있습니다. 그런데 만약 사용자가 데이터를 바꿔달라고 수정을 요청한다면 어떻게 될까요? "제 직업에 대한 설명을 바꿔주세요."와 같은 편지를 받았다고 생각해봅시다. view함수는 수정할 수 있는 권한이 있는지 확인하고 나서, 직업에 대한 설명을 수정해 다시 답장을 주겠지요. "완료했습니다!" 라고요. 그러고 나서 view는 답장을 생성하여, 장고는 그 답장을 그 사용자의 웹 브라우저에 보내주는 역할을 합니다.

## Web 간단 정리!
¬ Server
- HTML
- HTTP
- Port
- DNS: IP주소
- 데이터패킷: 라우터

## 가상환경 사용하기
$ python3 -m venv myvenv # 가상환경 생성
$ source myvenv/bin/activate # 가상환경 실행

### Terminal 명령어
- pwd / ls / cd / cd .. / mkdir  / cp / rm / exit

* 나의 첫 번째 Django 프로젝트!
- django-admin startproject mysite .

djangogirls
├───manage.py # 사이트 관리
└───mysite
        settings.py  # 웹사이트 설정
        urls.py # urlresolver가 사용하는 패턴 목록 포함
        wsgi.py
        __init__.py

# 서버 실행
python manage.py runserver 0.0.0.0:8000
- ctrl+c: 웹 서버 중지

# django의 model
- 객체의 특별한 종류
- 모델을 저장하면 내용이 db에 저장됨
- 모든 model 객체는 models.py에 선언해 모델을 만듦
- e.g.) 블로그 글 모델 (class Post)   

# migration
- 이제 데이터베이스에 우리의 새 모델, Post 모델을 추가할 거에요. 먼저 우리는 장고 모델에 (우리가 방금 만든!) 몇 가지 변화가 생겼다는 걸 알게 해줘야 합니다.
python manage.py makemigrations blog

- migration file  데이터베이스에 지금 반영할 수 있게 해줌
python manage.py migrate blog


# WSGI 프로토콜
장고는 WSGI 프로토콜을 사용해 작동한다. 이 프로토콜은 파이썬을 이용한 웹사이트를 서비스하기 위한 표준이다. WSGI 설정을 파일을 수정해 우리가 만든 장고 블로그를 PythonAnywhere에서 인식하게 해준다.

# 웹 개발 공통 작업 과정
이 것이 바로 공통적인 웹 개발의 작업 과정 입니다. 로컬에서 변경하고, 변경 사항을 GitHub에 적용하고, 변경 사항을 실제 웹 서버로 가져옵니다. 이를 통해 실제 웹 사이트를 손상시키지 않고 작업하고 테스트 해볼 수 있어요. 멋지지 않나요?



