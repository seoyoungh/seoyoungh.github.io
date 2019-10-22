---
title:  "Perceptron이란?"
excerpt: "Perceptron이 무엇인지 알아보자."
toc: true
toc_sticky: true
use_math: true

categories:
  - today-i-learned
tags:
  - machine-learning
  - deep-learning
  - programming
---
인공지능 수업에서 다룬 Perceptron을 정리하려 한다.

## Perceptron

![Screen Shot 2019-10-22 at 8.15.43 PM](/assets/images/Screen%20Shot%202019-10-22%20at%208.15.43%20PM.png)

퍼셉트론은 Neural Network 모형 중 하나로, 여러 input을 받아 하나의 output을 출력한다. 그 과정은 다음과 같다. 우선 input 각각에 weight를 적용해 곱한다. 여기서 weight은 뉴런에서 정보를 학습, 기억하고 전달하는 것과 같은 역할을 한다. 그리고 아래와 같이 input과 weight을 곱한 값들을 모두 합한다.

$$f(net)=f(w_0x_0+w_1x_1+w_2x_2)$$

**if net > θ then output = 1 else output = 0**

만약 net이 임계값을 넘으면 output이 1이고, 넘지 못하면 0이다. 이때 기준이 되는 임계값을 `Threshold`라고 부른다.

여기서 net은 `activation level`이다. 이 activation level이 threshold보다 높으면 `activate` 상태이다. 이 $f$를 우리는 `activation function`, threshold function이라고 부른다.

우리는 input에 맞게 output을 구하는 function $f(x)$를 찾는 것이 목표이다. 이 $f(x)$를 찾는다는 것은 곧 weights를 찾는 것이다. 그리고 이 과정을 학습 (learning) 이라고 한다!
