---
layout: post
title: "Perceptron이란?"
date: 2019-10-22
use_math: true
categories:
  - machine-learning
tags:
  - machine-learning
  - deep-learning
permalink: /:categories/:title/
---
인공지능 수업에서 다룬 Perceptron을 정리하려 한다.

<!-- {% include adsense.html %} -->

#### Perceptron

![Screen Shot 2019-10-22 at 8.15.43 PM](/assets/images/Screen%20Shot%202019-10-22%20at%208.15.43%20PM.png)

퍼셉트론은 Neural Network 모형 중 하나로, 여러 input을 받아 하나의 output을 출력한다. 그 과정은 다음과 같다. 우선 input 각각에 weight를 적용해 곱한다. 여기서 weight은 뉴런에서 정보를 학습, 기억하고 전달하는 것과 같은 역할을 한다. 그리고 아래와 같이 input과 weight을 곱한 값들을 모두 합한다.

$$f(net)=f(w_0x_0+w_1x_1+w_2x_2)$$

**if net > θ then output = 1 else output = 0**

만약 net이 임계값을 넘으면 output이 1이고, 넘지 못하면 0이다. 이때 기준이 되는 임계값을 `Threshold`라고 부른다.

여기서 net은 `activation level`이다. 이 activation level이 threshold보다 높으면 `activate` 상태이다. 이 $f$를 우리는 `activation function`, threshold function이라고 부른다.

우리는 input에 맞게 output을 구하는 function $f(x)$를 찾는 것이 목표이다. 이 $f(x)$를 찾는다는 것은 곧 weights를 찾는 것이다. 그리고 이 과정을 학습 (learning) 이라고 한다!

**if net > θ then output = 1 else output = 0**

여기서 θ를 $-b$로 치환해 넘겨 다음과 같이 표현할 수도 있다.

**if net + b > 0 then output = 1 else output = 0**

여기서 b를 우리는 bias라고 할 수 있다. 우리의 뉴런이 얼마나 쉽게 activate 되느냐를 조정하는 parameter이다.

<br/>

#### Limitations of the perceptron model

하지만 이 perceptron으로는 `non-linear` problem을 해결할 수 없다는 한계가 있다. 그 예시로, exclusive-or, XOR 문제를 들 수 있다. [XOR Problem에 대한 자세한 설명은 예전에 포스팅했다.](https://seoyoungh.github.io/deep-learnig-zero-to-all/zerotoall-7/)

이를 해결하기 위해 우리는 data를 나누기 위해 두 개의 line을 사용할 수 있다. 두 개의 line은 즉, 두 개의 node를 사용한다는 것이다. 이렇게 여러 층으로 이루어진 퍼셉트론을 `multilayered perceptron`이라고 부른다. 이런 다층 퍼셉트론에는 non-linear activation function이 필요하다.

![Screen Shot 2019-10-22 at 8.54.02 PM](/assets/images/Screen%20Shot%202019-10-22%20at%208.54.02%20PM.png)

여기서 첫 번재 layer는 input을 linearly seperable하게 만드는 역할을 한다.
