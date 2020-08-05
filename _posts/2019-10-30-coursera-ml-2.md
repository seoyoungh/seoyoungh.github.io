---
title:  "Linear Regression with Multiple Variables"
excerpt: "(Coursera) Machine Learning offered by Stanford "
toc: true
toc_sticky: true
use_math: true

categories:
  - machine-learning
tags:
  - machine-learning
  - coursera
---
Andrew Ng 교수님의 Coursera 강좌 [Machine Learning offered by Stanford](https://www.coursera.org/learn/google-machine-learning?) Week 2 에 해당하는 내용입니다.

**19/10/30 시작!**

수업 시작에 앞서 MATLAB Online과 Octave 환경 구축을 완료했다.

# Multivariate Linear regression

## Multiple Features
![Screen Shot 2019-10-30 at 5.30.51 PM](/assets/images/Screen%20Shot%202019-10-30%20at%205.30.51%20PM.png)

![Screen Shot 2019-10-30 at 5.31.04 PM](/assets/images/Screen%20Shot%202019-10-30%20at%205.31.04%20PM.png)

## Gradient Descent for Multiple Variables

앞서 공부한 single linear regression의 cost function의 식은 다음과 같다. multi linear regression의 cost function도 동일하다. parameter의 수가 증가했지만, 각각의 cost function을 구하면 된다.

$$J(θ0,θ1)=\frac{1}{2m}\sum_{i=1}^{m}(\hat y_i−y_i)^2=\frac{1}{2m}\sum_{i=1}^{m}(h_θ(x_i)−y_i)^2$$

이 cost function을 미분한 것에 learning rate를 곱해 이전의 parameter 값에서 빼준 후 parameter 값을 업데이트 해주는 것이 GDA였다. 구체적인 과정은 다음과 같다. **$x_0$는 1로 둔다.**

![Screen Shot 2019-10-30 at 5.47.23 PM](/assets/images/Screen%20Shot%202019-10-30%20at%205.47.23%20PM_r7wxuawhp.png)

[Cost 함수를 미분하는 과정은 여기에 잘 나와있다.](http://www.birc.co.kr/2018/01/15/gradient-descent-algorithm/)

## Feature Scaling
여러개의 feature가 있을 때, feature의 단위 크기가 비슷하다면, 여러 feature의 범위가 같다면 gradient descent는 더 빠르게 수렴할 수 있다.

![Screen Shot 2019-10-30 at 6.08.34 PM](/assets/images/Screen%20Shot%202019-10-30%20at%206.08.34%20PM.png)

이 경우 $x_1$과 $x_2$의 단위 크기 차이가 커서, 등고선을 그리면 길쭉한 타원형 형태가 된다. 이러면 minimum을 찾기까지 매우 오랜 시간이 걸린다. 이를 오른쪽과 같이 scaling해주면, 두 feature 둘 다 0과 1사이의 값을 갖게 조정해줄 수 있다. 그러면 예쁜 등고선이 그려져서 더욱 빠르게 minimum을 찾을 수 있다.

보통은 모든 feature를 적절한 수로 나누어 모든 값이 대략 `-1에서 1 사이`에 있게 한다.

또 다른 방법은, `Mean normalization`이다. 다음과 같이 $x_i$를 바꾸어준다.

$$x_i := \frac{x_i −μ_i}{s_i}$$

Where $μ_i$ is the average of all the values for feature (i) and $s_i$ is the range of values (max - min), or $s_i$ is the standard deviation.

## Learning Rate
​
### Debugging
만약 GDA가 잘 작동한다면, 매 iteration마다 $J(\theta)$가 감소해야 한다. 만약 특정 시점 이후에 cost function이 더이상 감소하지 않았다면, 그 시점에서 이미 수렴한 것이다. 수렴까지 걸리는 반복 횟수는 다 다르다.

수렴 여부 확인을 위해서는 그래프를 그려 확인할 수도 있다. 또다른 방법으로 automatic convergence test를 진행할 수도 있다. 예로, 만약 한 번 반복했을 때 0.001보다 작게 감소하면 수렴했다고 판단할 수 있다. 하지만 이 임계값을 결정하는 것도 어려운 일이다. 따라서, 보통 그래프를 그려 판단한다.

만약 점차 감소하지 않는 그래프를 그린다면, 이는 $\alpha$를 수정해야 한다는 경우이다. 오히려 증가하거나, 감소하고 증가하는걸 반복하는 경우 모두에 해당한다.

learning rate에 따른 그래프 형태에 관한 예제를 첨부한다.

![Screen Shot 2019-10-30 at 6.27.11 PM](/assets/images/Screen%20Shot%202019-10-30%20at%206.27.11%20PM.png)

### How to choose learning rate $\alpha$

교수님은 약 3배씩 늘려가며 learning rate를 수정해나가라고 제안하셨다.

..., 0.001, 0.003, 0.01, 0.03, 0.1, 0.3, 1, ...

정리하면,
* If α is too small: slow convergence.
* If α is too large: ￼may not decrease on every iteration and thus may not converge.

따라서, 계속 그래프를 확인해가며 적절한 learning rate를 찾자.

## Features and Polynomial Regression
우리의 hypothesis는 linear하지 않아도 된다. 선형 회귀를 이용하여 복잡한 비선형 함수에도 적용해볼 수 있다.

예로, $x_1$과 $x_2$를 조합해 새로운 feature인 $x_3$을 만들 수 있다. 또는, 아래와 같이 $x_1$하나를 변형시켜 삼차식 또는 square root function을 만들 수도 있다.
​
![Screen Shot 2019-10-30 at 6.38.51 PM](/assets/images/Screen%20Shot%202019-10-30%20at%206.38.51%20PM.png)

이때 feature scaling은 더욱 중요해진다. 범위에 맞게 잘 조정해주어야 한다. 관련 예제를 첨부한다.

![Screen Shot 2019-10-30 at 6.35.34 PM](/assets/images/Screen%20Shot%202019-10-30%20at%206.35.34%20PM.png)

## Normal Equation
이 방법은 특정 선형 회귀 문제에서 파라미터 $\theta$를 구하는데 효과적인 방법이다.

In the `Normal Equation` method, **we will minimize J by explicitly taking its derivatives with respect to the $θ_j$’s, and setting them to zero.** This allows us to find the optimum theta without iteration. The normal equation formula is given below:

$$θ=(X^TX)^{-1}X^Ty$$

Octave에서는 다음과 같이 실행한다.

```MATLAB
pinv(X'*X)*X'*y
```

`Normal Equation`을 사용하면, feature scaling을 하지 않아도 된다. GDA와 Normal Equation을 비교하면 다음과 같다.

![Screen Shot 2019-10-30 at 7.41.03 PM](/assets/images/Screen%20Shot%202019-10-30%20at%207.41.03%20PM.png)	 

Normal Equation은 비교적 간단하지만, 역행렬 계산 때문에 n이 증가하면 느려진다. n이 10000이상이라면 GDA를 사용하는 것이 좋다.

대부분 역행렬을 갖지만, 역행렬을 갖지 않는 비가역행렬(non-invertible matrix)이 존재할 수 있다.

If $(X^TX)$ is noninvertible, the common causes might be having :

* Redundant features, **where two features are very closely related** (i.e. they are linearly dependent)
* Too many features (e.g. m ≤ n). In this case, **delete some features or use `regularization`** (to be explained in a later lesson).

When implementing the normal equation in octave we want to use the 'pinv' function rather than 'inv.' The 'pinv' function will give you a value of θ even if $(X^TX)$ is not invertible.

# Octave/Matlab Tutorial

**19/10/31 끝!**
