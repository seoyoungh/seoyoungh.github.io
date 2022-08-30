---
layout: post
title: "추천 시스템의 종류"
date: 2021-03-11
use_math: true
categories:
  - machine-learning
  - recommender-systems
tags:
  - machine-learning
  - recommender-systems
permalink: /:categories/:title/
---
추천 시스템을 개괄적으로 다룬 논문을 짧게 요약한 것입니다.

<!-- {% include adsense.html %} -->

### The Survey of Recommender Systems
- rely on the ratings structure
- the problem: estimating ratings of **non-rated** items

<br/>

#### Utility function
- measures the usefulness of item `s` to user `c`
- want to choose `s` to maximizes the users's Utility
- utility is represented by a rating

<br/>

##### 문제점
- 전체 C*S space에서 정의되는 것이 아니라, only on subset of it! 유저들이 rated 했던 아이템에 대해서만 정의됨
- **Recommendation engine should be able to estimate the ratings of the nonrated item/user combination**

<br/>

##### 해결방법
1) specifying heuristics that define the utility function
2) estimating the utility function that optimizes certain performance criterion
- machine learning, approximation theory, various heuristics ...

<br/>

#### 추천시스템 종류
- Content-based: 과거에 선호했던 아이템과 유사한 아이템을 찾아 추천
- Collaborative filtering: 해당 유저와 가장 유사한 취향, 선호를 가진 사람들이 과거에 좋아했던 아이템을 추천
- Hybrid approaches: Content-based + Collaborative filtering
- cf) preference-based filtering: predicting the `relative` preferences of users

<br/>

#### Content-based
- usually focus on recommending items containing textual information
- the content is usually described with keywords, and calculate the importance of those keywords in the document
- **TF-IDF**: 다른 문서에는 잘 안나오지만 그 문서에서 상대적으로 많이 나오는 term의 importance를 weight으로 나타냄
- **Cosine Similarity**: 추천할 item vector와 user taste vector의 유사도를 계산 (heuristic method)
- measure the similarity between vectors of TF-IDF weights
- **Based on model**: statistical learning, machine learning

<br/>

##### 문제점
1) Limited Content Analysis
2) Overspecialization
3) New User Problem

<br/>

#### Collaborative Filtering
- predict the utility of items previously rated by other users
- tries to find the peers of user
1) memory-based
- essentially are heuristics
- the value of the unknown ratings -> computed as an aggregation of previously rated items
- (average, weighted sum, adjusted weighted sum)
- the similarity between two users -> based on their ratings of items that both users have rated
- (correlation, cosine-based)
- measures the similarity between vectors of the actual user-specified ratings

2) model-based
- cluster models, Bayesian networks, a probabilistic relational model, linear regression

<br/>

##### 문제점
1) New User Problem
2) New Item Problem
3) Sparsity: user가 많아야 하고 user가 items를 많이 rated 했어야 함, 보완하기 위해 demographic 정보 사용 or dimensionality reduction technique

<br/>

#### Hybrid Methods
- 다양한 방법으로 둘을 조합해 사용할 수 있음
