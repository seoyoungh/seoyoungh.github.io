---
layout: post
title: "docker image 배포시 권한이 계속 거절당하는 issue"
date: 2020-04-24
use_math: true
categories:
  - today-i-learned
tags:
  - docker
permalink: /:categories/:title/
---
맥 유저분들! requested access is denied 때는 이렇게 해결하세요!

<!-- {% include adsense.html %} -->

Datacenter programming 수업에서 직접 만든 docker image를 docker hub에 deploy하려는데, 계속 아래와 같은 이슈가 발생했다.

```
denied: requested access to the resource is denied
```

![Screen Shot 2020-04-24 at 1.20.57 AM](/assets/images/Screen%20Shot%202020-04-24%20at%201.20.57%20AM.png){: width="60%" height="60%"}

구글링해보니 나와 같은 이슈를 겪고 있는 사람들이 많았다. Linux에서는 발생하지 않는 이슈고, 보통 macOS에서 이런 이슈가 발생하는 것 같았다. dockerhub에 로그인이 되지 않은 경우에 위와 같은 오류가 발생한다고 했다. 그런데 나는 로그인이 아주 잘 되어 있었다!

또 어디선 비밀번호에 특정 특수문자가 들어가 있는 경우에 오류가 생긴다는 말이 있었는데, 나 역시도 ``@``를 포함하고 있었다. 그래서 비밀번호를 바꾸었는데, 해결되지 않았다 😭

그러다 이 [stackoverflow](https://stackoverflow.com/questions/41984399/denied-requested-access-to-the-resource-is-denied-docker) 페이지에서 해답을 찾을 수 있었다!

결국 요점은 docker에서 빌드할 때, ``username/image-name``으로 이름을 설정해야 한다.

```
$ docker push my-nginx:1.0
```
이 아니라
```
$ docker push seoyoungh/my-nginx:1.0
```
로 빌드해야 한다는 것이다.

이렇게 빌드한 후에, (로그인은 마쳤다고 가정한다.)

```
$ docker tag seoyoungh/my-nginx:1.0 my-nginx:1.0
```
로 local의 image를 dockerhub의 새로운 repository와  태깅해주고,

```
$ docker push seoyoungh/my-nginx:1.0
```
이 명령을 수행하면, 정상적으로 dockerhub에 내가 만든 docker image를 push할 수 있다.

![Screen Shot 2020-04-24 at 1.29.40 AM](/assets/images/Screen%20Shot%202020-04-24%20at%201.29.40%20AM.png){: width="80%" height="80%"}

my-nginx 배포때는 캡쳐하지 못해 my-django push 결과 화면을 첨부한다 😀
