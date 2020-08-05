---
title:  Basic Unix Commands
excerpt: 기본 유닉스 커맨드
toc: true
toc_sticky: true
use_math: true

categories:
  - today-i-learned
tags:
  - programming
  - unix
  - mac
---

## Unix Commands

- cd
- cd ..
- ls
- pwd
- mkdir
- (file) cp (copy) rm (remove)
- (directory) cp -r rm -r
- cat (전체 파일 프린트)
- touch (empty file 생성)
- head / tail
- > / >>
  - e.g.) python3 example.py > example.txt

```
#!/bin/bash

python3 example.py 1 > example.txt
python3 example.py 2 >> example.txt
```

- shell script는 .sh로 생성
- `chmod +x run.sh` 권한 부여
