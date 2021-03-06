---
title:  "Django 프로젝트 시작하기!"
excerpt: "Django Girls Tutorial - 나만의 블로그 만들기"
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

### Django 프로젝트 시작하기!
`$ source myvenv/bin/activate` 가상환경으로 접속한 후, terminal에서 다음과 같이 입력한다.
`django-admin startproject <project name> .`

`django-admin.py`은 스크립트로 디렉토리와 파일들을 생성한다.

그러면 다음과 같은 디렉토리 구조를 볼 수 있다.
```
djangogirls
├───manage.py # 사이트 관리
└───mysite
        settings.py  # 웹사이트 설정
        urls.py # urlresolver가 사용하는 패턴 목록 포함
        wsgi.py
        __init__.py
```

- `manage.py`는 스크립트인데, 사이트 관리를 도와주는 역할을 한다. 이 스크립트로 다른 설치 작업 없이, 컴퓨터에서 웹 서버를 시작할 수 있다.
- `settings.py`는 웹사이트 설정이 있는 파일이다. 이 파일을 수정해 설정 변경을 할 수 있다.
- `urls.py`파일은 urlresolver가 사용하는 패턴 목록을 포함하고 있다.

### 데이터베이스 생성하기
우리가 사용할 `sqlite3`는 이미 `mysite/settings.py`파일 안에 설치가 되어있다.
`python manage.py migrate` 명령을 실행해 데이터베이스를 생성한다.

### 서버 실행
`python manage.py runserver` 명령을 실행해, 웹 서버를 바로 시작할 수 있다.
`python manage.py runserver 0.0.0.0:8000`
- `ctrl+c`: 웹 서버 중지
- 웹 서버가 실행되는 동안 추가 명령은 실행되지 않으므로, 추가 명령을 하고 싶다면 새 터미널 창을 열어야 한다.

### Django의 model
- 객체의 특별한 종류
- 모델을 저장하면 내용이 db에 저장됨
- 장고의 기본 db는 `sqlite`
- 모든 model 객체는 `models.py`에 선언해 모델을 만듦
- e.g.) 블로그 글 모델 (class Post)   

### 어플리케이션 만들기
앱을 만들기 위해 아래 명령어를 실행한다.
`$ python manage.py startapp <app name>`

이번 경우에 `blog`라는 어플리케이션을 만들었다.

앱을 생성한 후 장고에게 사용한다고 알려주어야 하는데, `mysite/settings.py` 파일 안의 `INSTALLED_APPS` 부분에 방금 만든 앱 이름을 추가해주면 된다.

### 블로그 글 모델 만들기
 모든 모델 객체는 `models.py`에 선언하여 모델을 만드므로, 우리는 `blog/models.py`에 블로그 글 모델을 정의할 것이다. 다음과 같은 코드를 해당 파일에 추가했다. Post라는 모델을 정의하는 코드이다. 자세한 코드 설명은 생략하겠다.

 ```python
 from django.conf import settings
from django.db import models
from django.utils import timezone


class Post(models.Model):
    author = models.ForeignKey(settings.AUTH_USER_MODEL, on_delete=models.CASCADE)
    title = models.CharField(max_length=200)
    text = models.TextField()
    created_date = models.DateTimeField(
            default=timezone.now)
    published_date = models.DateTimeField(
            blank=True, null=True)

    def publish(self):
        self.published_date = timezone.now()
        self.save()

    def __str__(self):
        return self.title

 ```

### Migration
이제 데이터베이스에 우리의 새 모델, Post 모델을 추가해야 한다. 먼저 우리는 다음과 같은 명령어를 실행해 장고 모델에 몇 가지 변화가 생겼다는 걸 알게 해줘야 한다.
`python manage.py makemigrations blog`

- migration file: 데이터베이스에 지금 반영할 수 있게 해주는 파일

아래와 같은 명령을 실행해, 데이터베이스에 모델 추가를 반영할 수 있다.
`python manage.py migrate blog`

이 과정을 통해 Post 모델이 데이터베이스에 저장되었다.

### 장고 관리자
`blog/admin.py` 파일을 열어 아래와 같이 수정하면, 관리자 페이지에서 만든 모델을 볼 수 있다.

``` python
from django.contrib import admin
from .models import Post

admin.site.register(Post)
```
콘솔에서 `python manage.py runserver` 명령을 실행해 웹 서버를 실행한다. 브라우저에 `http://127.0.0.1:8000/admin/`을 입력하면 로그인 페이지를 볼 수 있다.

`python manage.py createsuperuser` 명령어를 입력하고, 사용자 이름과 비밀번호를 입력해주면 superuser계정을 만들 수 있다.
