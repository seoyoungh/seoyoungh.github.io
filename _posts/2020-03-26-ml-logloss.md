---
layout: post
title: "Log loss란?"
date: 2020-03-26
use_math: true
categories:
  - machine-learning
tags:
  - machine-learning
  - deep-learning
permalink: /:categories/:title/
---

<!-- {% include adsense.html %} -->

#### Loss function (손실 함수)란?
**Cross-Entropy** 라고도 불린다.

모델의 출력값과 정답의 오차를 정의하는 함수이다. 신경망을 학습할 때, 학습이 잘 되고 있는지 평가하는 하나의 지표로 사용된다. 결국 신경망의 성능이 얼마나 나쁜지를 나타내는 지표이다.

<br/>

#### Log loss란?

* 모델 성능 평가 시 사용 가능한 지표
* 분류(Classification) 모델 평가시 사용합니다.

<br/>

##### 왜 사용하는가?
최종적으로 맞춘 결과만 가지고 성능을 평가할 경우, 얼만큼의 확률로 해당 답을 얻은건지 평가가 불가능하다. 답은 맞췄지만 20%의 확률로 그저 찍은거라면 성능이 좋은 모델이라고 할 수 없을 것이다.

이를 보완하기 위해서는 확률 값을 평가 지표로 사용하면 된다. Log loss는 모델이 예측한 확률 값을 직접적으로 반영하여 평가한다.

확률 값을 음의 log함수에 넣어 변환을 시킨 값으로 평가하는데, 이는 잘못 예측할 수록, 패널티를 부여하기 위함이다.

예로, 100%의 확률(확신)로 답을 구한 경우 log loss는 -log(1.0) = 0이다. 80% 확률의 경우에는, -log(0.8) = 0.22314이다. 60% 확률의 경우에는, -log(0.6) = 0.51082이다.

확률이 낮아질 수록 log loss 값이 기하급수적으로 증가하는 것을 볼 수 있다. 이런식으로 log loss는 확률이 낮을 때 패널티를 더 많이 부여하기 위해 음의 로그 함수를 사용한다.

<br/>

##### 모델 전체의 Log loss를 구하려면?
실제 답안에 해당하는 확률 값을 음의 로그를 취해 모두 더하고 1/n해서 평균을 내면된다. 이렇게 최종적인 모델의 log loss를 산출할 수 있다.

<br/>

#### 다른 loss function

##### MSE (Mean Squared Error)
모델의 출력값과 실제 정답의 차이를 제곱하고 이 값들을 모두 합한다. 그리고 미분을 쉽게 하기 위해 1/2을 해주면 된다.

출력값과 정답이 연속적인 수치인 경우에 잘 맞기 때문에 주로 회귀분석에서 사용된다!ㄴ