---
title:  "machine learning 기초"
excerpt: "Sung Kim 교수님 강의로 공부하는 머신러닝"
toc: true
toc_sticky: true
use_math: true

categories:
  - deep-learnig-zero-to-all
tags:
  - machine-learning
---
~~아직 작성 중인 문서입니다.~~

## Machine Learning
### 등장 배경
> 명시적인 프로그래밍(explicit programming)의 한계를 느끼기 시작했다.

Spam detection이나, 자율주행의 경우 rule이 너무 많아 explicit programming을 적용하기 어렵다. 하지만, 머신러닝은 `학습`하고, `자동화`되는 프로그래밍으로, 이런 문제들을 해결하기에 적합하다.

### Supervised v.s. Unsupervised
> 학습 방법에 따라 supervised learning과 unsupervised learning으로 나뉜다.

1. Supervised Learning
* most common problem type of ML
* learning with labeled examples - training set
* 예로 Image labeling, Spam filtering(spam or pam), Predicting exam score이 있다.
* 대표적인 기법으로는 regression, classification이 있다.
* `classification`은 label의 개수에 따라 binary(class 2개), multi-label(class 3개 이상)로 구분된다.

2. Unsupervised Learning
* 예로는 News grouping, Word clustering이 있다.

### Training set(data) v.s. Test set(data)
> Modeling에 사용되는 데이터를 training data, 모델을 만든 후 성능을 검증할 때 쓰는 data를 test data라고 한다. 보통 6:4 또는 7:3의 비율로 나눈다.

## Linear regression
> x와 y가 `linear relationship`을 가진다고 판단이 들 때, 일차방정식 형태의 가설을 세워 모델링하는 것이다.

### Hypothesis
$H(x)=Wx+b$
가설은 일차방정식의 형태를 띈다. W는 weight, slope(기울기)이고 b는 bias, intercept(절편)이다.  
`Simplified hypothesis`: 이를 간소화해서 $H(x)=Wx$로 나타내기도 한다.

### Residual(잔차)
> 잔차는 $H(X)-y$, 모델에서 예측한 값 - 실제 예측한 값이다. 

### RSS(residual sum of squares)
잔차는 음수가 될 수도, 양수가 될 수도 있기 때문에 square처리해서 모든 잔차를 더한다. RSS를 식으로 나타내면 ${H(X)-y}^2$이다.

### Cost function
> $cost(W,b) = 1/m * \sum_{i=n}^m (H(X^i)-y^i)^2$

좋은 모델을 위해서는 잔차를 최소화 해야한다. 이 잔차 합의 평균을 구하는 함수를 `cost function`이라고 부르는데, **이 cost를 minimize 하는 w,b를 찾아야한다.**

`Simplified cost function`: bias를 고려하지 않고 $cost = 1/m * \sum_{i=n}^m (W(X^i)-y^i)^2$로 나타내기도 한다.

Cost function은 Loss function이라고도 불린다.

### Gradient descent algorithm(경사 하강법)
> Cost function을 minimize하는 w,b를 찾아내는 알고리즘

`Gradient`는 `경사`를, `Descent`는 `내려간`을 의미한다. 경사도를 따라서 내려가다가 경사도가 0이 되었을 때 stop하는 알고리즘이라고 할 수 있다. 

* 0,0에서 시작(또는 다른 값에서 시작)
* W,b 을 조금 바꾸고 줄일 수 있는지 확인한다.
* 파라미터(W,b)를 바꿀때마다 cost(W,b)를 가장 줄일수 있는 경사도(gradient)를 선택한다.
* 미분을 이용해 구하는데, tensorflow에서 자체적으로 구해주기 때문에 걱정 안해도 된다.

>W := W - a(cost(W)를 미분한 값)

a(alpha)는 보통 learning rate

descent가 +이면, -로 이동 / descent가 -이면, +로 이동

### Convex function
> 시작점에 상관없이 도착점이 같은 function

Cost function은 convex function이여야 한다. 확인하고 GDA를 사용해야한다!

## Multi-variable linear regression
> x1, x2, x3와 같이 여러개의 input이 있는 multi-variable regression  

### Hypothesis
$H(x1,x2,x3)=w1x1+w2x2+w3x3+b$

*Matrix multiplication*으로 표현하면 다음과 같다.
$H(X)=XW$

[X] * [W] = [H(X)]
[instance 개수, variable 개수] * [?, ?] = [instance 개수, Y 개수]
[instance 개수, variable 개수] * *[variable 개수, Y 개수]** = [instance 개수, Y 개수] 

#### WX v.s. XW
Theory: $H(x)=Wx+b$
Implementation(Tensorflow): $H(X)=XW$

둘은 같지만, 실제로 텐서플로에서는 두번째 식을 사용한다. 

### Cost function
Sigmoid function은 Convex function이 아니다! Local minimum, Global minimum이 다를 수 있다. 따라서, cost function을 새로 만들어준다. exponentional과 상반되는 log를 취해준다.

$C(H(x),y)=$

**(y=1)** $-log(H(x))$  
> 로그함수의 모양에 따라 H(x)가 1이라면 cost는 0이 나온다. 반면, H(x)가 0이라면 cost는 무한으로 커진다.

**(y=0)** $-log(1-H(x))$ 
> 로그함수의 모양에 따라 H(x)가 0이라면 cost는 0이 나온다. 반면, H(x)가 1이라면 cost는 무한으로 커진다.

$C(H(x),y)=-ylog(H(x))-(1-y)log(1-H(x))$



## Classification






