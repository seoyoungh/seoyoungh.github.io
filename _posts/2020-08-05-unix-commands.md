---
layout: post
title: "Basic Linux Commands (기본 리눅스 커맨드)"
date: 2020-08-05
use_math: true
categories:
  - today-i-learned
tags:
  - dev
  - unix
  - mac
permalink: /:categories/:title/
---

<!-- {% include adsense.html %} -->

#### Unix Commands
- cd
- cd .. # 상위 폴더로 이동
- ls
- pwd
- mkdir
- `file` cp (copy) rm (remove)
- `directory` cp -r rm -r
- cat # 전체 파일 프린트
- touch # empty file 생성
- head / tail

- `>`: 덮어쓰기
- `>>`: append

```
#!/bin/bash

python3 example.py 1 > example.txt # example.py 실행결과를 example.txt로 만)기
python3 example.py 2 >> example.txt # example.py 실행결과를 example.txt에 추가하기
```

- shell script는 .sh로 생성
- `chmod +x run.sh` 권한 부여
