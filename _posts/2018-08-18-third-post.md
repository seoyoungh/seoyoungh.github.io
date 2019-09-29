---
title:  "tensorflow 기초"
excerpt: "Sung Kim 교수님 강의로 공부하는 머신러닝"
toc: true
toc_sticky: true
use_math: true

categories:
  - deep-learnig-zero-to-all
tags:
  - machine-learning
  - tensorflow
---
~~아직 작성 중인 문서입니다.~~

### Tensorflow
> an open source software library for numerical computation using data flow graphs

* 구글이 만든 오픈소스 라이브러리
* Machine learning, artificail intellegence를 위한 python library

## Data Flow Graph
> Node와 Edge로 이루어진 flow graph

* `Node`: mathematical `operation`
* `Edge`: `tensor`(multidimensional data arrays), data

## TensorFlow Mechanics
> Node and Session
1. Build graph(tensors) using TF operations
2. Feed data and run graph(operation)
* `sess.run(op)`
`Node`를 placeholder라는 특별한 node로 만들 수 있다.
* `sess.run(op, feed_dict={x: x_data})`
3. Update variables in the graph and return values

## Tensor Ranks, Shapes, and Types
* Rank: 차원
    * Rank 0: scalar = 4
    * Rank 1: vector = [1, 2, 3]
    * Rank 2: Matrix = [[1,2,3], [4,5,6]]
    * Rank 3: 3-Tensor = [[[2],[4],[6]]]
    * Rank n: n-Tensor = ...
* Shape: element number, dimension number
    * 0-D: [] (scalar)
    * 1-D: [5]
    * 2-D: [3,4]
    * n-D: [1,3,..,n]
* Type
    * float, double, int...
* Example
    * [[1,2,3], [4,5,6]]: Rank 2, Shape [2, 3]
    * [[[1., 2., 3.]], [[7., 8., 9.]]] Rank 3, Shape [2,1,3]

## Variable
>우리가 흔히 아는 변수가 아닌, tensorflow가 학습하는 과정에서 자체적으로 변경시키는 trainable한 variable

``` python
W = tf.Variable(tf.random_normal([1]), name="weight")
b = tf.Variable(tf.random_normal([1]), name="bias")
```




*모든 코드는 [Sung Kim 교수님의 Github](https://github.com/hunkim/DeepLearningZeroToAll)에서 확인하실 수 있습니다.*
