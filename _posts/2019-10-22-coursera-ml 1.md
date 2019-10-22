---
title:  "Welcome to Machine Learning!"
excerpt: "(Coursera) Machine Learning offered by Stanford "
toc: true
toc_sticky: true
use_math: true

categories:
  - coursera-machine-learning
tags:
  - machine-learning
  - tensorflow
---
Andrew Ng 교수님의 Coursera 강좌 [Machine Learning offered by Stanford](https://www.coursera.org/learn/google-machine-learning?) Week 1 에 해당하는 내용입니다.

시작 전 여담이지만, 이 강좌를 내가 수강할 당시 약 250만 명이 들었다고 했다. 그만큼 좋은 강의라는 걸 보여주는 지표이기도 하고, 머신러닝에 대한 관심이 얼마나 뜨거운지를 보여주기도 한다. 10월 22일부터 시작해, 딱 2달 간 진행해서 12월 22일까지 모두 수강하는 것이 목표이다 :) 열심히 들어서 Certificate 받아보자!

![Screen Shot 2019-10-22 at 6.26.41 PM](/assets/images/Screen%20Shot%202019-10-22%20at%206.26.41%20PM.png)

ㅋㅋ 모듈의 밋앤그릿에 글을 남겨보았다! Go for it!

# Introduction

## Machine learning definition
- Arthur Samuel (1959): the field of study that gives computers the ability to learn without being explicitly programmed
- Tom Mitchell (1998): Well-posed Learning Problem: A computer program is said to learn from `experience E` with respect to some `task T` and some `performance measure P`, if its performance on T, as measured by P, improves with experience E.
  - Example: playing checkers.
  - E = the experience of playing many games of checkers
  - T = the task of playing checkers.
  - P = the probability that the program will win the next game.

## Machine Learning examples
- Handwriting recognition
- Natural Language Processing (NLP)
- Computer Vision
- Self-customizing programs (e.g., Amazon, Netflix)
- Understanding human learning (brain, real AI)

## Machine Learning algorithms
- Supervised learning: task를 수행할 수 있는 방법을 컴퓨터에게 가르침
- Unsupervised learning: 컴퓨터가 스스로 학습하도록 유도
- Reinforcement Learning
- Recommender systems

### Supervised learning
- `right answers` given
- `Regression`: Predict continuous valued output
- `Classification`: Discrete valued output (0 or 1)
  - 분류에 쓰이는 속성이 1개일 수도 있고, 여러 개일 수도 있다.

### Unsupervised learning
- `Clustering`: 관련이 있는 것끼리 묶어주는 것
- e.g. social network analysis, market segmentation, astronomical data analysis

**Cocktail party problem algorithm**

Unsupervised learning이 적용된 예시로, 두 개의 음성 소스가 합쳐진 파일에서 각각의 음성 소스를 분리해내는 알고리즘이다. 놀랍게도 아래의 단 한 줄의 Octave 코드로 구현이 가능하다!

```
[W,s,v] = svd((repmat(sum(x,*x,1),size(x,1),1).*x)*x');
```

여기까지 전체적으로 다 아는 내용이여서, 간략하게 정리했다.
