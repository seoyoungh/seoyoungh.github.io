---
layout: post
title: "Introduction of Recommender systems"
date: 2021-04-14
use_math: true
categories:
  - machine-learning
  - recommender-systems
tags:
  - machine-learning
  - recommender-systems
permalink: /:categories/:title/
---
전반적인 추천 시스템에 대해 알아보자! Recommender systems 원서에서 발췌했습니다.

<!-- {% include adsense.html %} -->

## Recommender Systems
### 1.1 Introduction
- Web의 등장으로 유저가 five-star ratings, like or dislike 등으로 feedback을 쉽게 제공할 수 있게 됨
- Recommendation analysis is often based on **the previous interaction between users and items**
- **past interests & proclivities** -> good indicators of future choices
- knowledge-based recommender system의 경우, past history보다는 user-specified requirements에 따라 추천
- the basic principle: significant dependencies exist between user- and item-centric activity
- various categories of items may show significant correlations

<br/>

#### 추천 시스템 종류
- neighborhood models
  - **collaborative filtering**
    - input: User ratings + community ratings
    - the use of ratings from multiple users in a collaborative way to predict missing ratings
    - work with data which is the information about the users and items such as textual profiles or relevant keywords
- **content-based** recommender systems
  - input: User ratings + item attributes
  - user interests can be modeled on the basis of attributes of the items they've rated or accessed in the past
  - work with data which is the user-item interactions, such as ratings or buying behavior
- **knowledge-based** recommender systems
  - input: User specification + item attributes + domain knowledge
  - specify their interests and the user specification is combined with domain knowledge

<br/>

### 1.2 Goals of Recommender Systems
#### Two primary models
##### 1. Prediction version of problem
- to predict the rating value for a user-item combination
- matrix completion problem
- incompletely specified matrix of values, and the remaining values are predicted by the learning algorithm

<br/>

##### 2. Ranking version if problem
- top-k recommendation problem
- ranking formulation of the recommendation problem
- not necessary to predict the ratings of users for specific items
- just recommend the top-k items for particular user, or the top-k users to target for a particular item
- recommend the top-k items -> more popular
- the absolute values of the predicted ratings are not important

<br/>

#### The primary goals
- **increasing product sales and profits**

<br/>

#### Operational and technical goals
##### 1. Relevance
- the most obvious operational goal
- to recommend items that are relevant to the user

<br/>

##### 2. Novelty
- 유저가 과거에 보지 못한 아이템을 추천하면 good
- 단순히 popular한 아이템 추천을 반복하는 것은 sales diversity를 떨어뜨림

<br/>

##### 3. Serendipity
- 유저가 평소에 선호하던 것과는 다르지만, 유저를 정말 놀래킬만한 것
- truly surprising to the user, rather than simply something they did not know about before
- increasing sales diversity or beginning a new trend of interest
- longer term and strategic benefits

<br/>

##### 4. Increasing recommendation diversity
- 비슷한 추천만 하면 안되고 다양한 type의 아이템을 추천 리스트에 포함시켜야 함

<br/>

#### Other goals
- help improve overall user satisfaction
- **explanation for why a particular item is recommended**
  - e.g.) previously watched movies

<br/>

#### Example of products recommended
- GroupLens: News
  - pioneering recommender system
  - BookLens, MovieLens
- Amazon.com: Books and other products
  - implicit ratings: purchase or browsing behavior of a user
  - providing recommendations both on the basis of explicit and implicit feedback
- Netflix: Videos
  - providing explanations
- Google News: News
  - implicit ratings
- Facebook: Friends, Advertisements
  - **link prediction**
  - based on structural relationships

<br/>

#### Trends
- Traditional domain of recommender systems: traditional e-commerce applications for various products (books, movies, videos, other goods and services)

- 최근에는 이러한 상품에 국한되지 않고 domain이 다양해짐
  - Facebook
    - recommends friends, not products
  - Google Search
    - computational advertising
    - 검색 결과와 관련있는 상품을 광고
    - 추천과 같지는 않지만 closely related to recommender systems

<br/>

### 1.3 Basic Models of Recommender Systems
#### 1.3.1 Collaborative Filtering Models
- 문제점: the underlying rating matrices are sparse, most of the ratings are unspecified (unobserved)
- can be viewed as generalizations if classification and regression modeling
- there is no distinction between training and test rows in collaborative filtering because any row might contain missing values
  - training and test entries (O)
  - training and test rows (X)

<br/>

##### 1) Memory-based methods
- **similarity-based models**
- Two types
  - User-based: 유저와 유사한 유저를 찾음
  - Item-based: 유저가 선호하는 아이템과 유사한 아이템을 찾음
- 장점: simple to implement and the resulting recommendations are often easy to explain
- 한계: do not work very well with sparse rating matrices

<br/>

##### 2) Model-based methods
- machine learning and data mining methods are used in the context of predictive models

<br/>

#### 1.3.2 Content-based Recommender Systems
- the descriptive attributes of items are used to make recommendations
- `content` refers to `descriptions`
- 장점
  - 충분한 rating이 존재하지 않아도 추천 제공 가능
  - provide obvious recommendations because of the use of keywords or content
- 약점
  - they are not effective at providing recommendations for new users
  - 오버피팅 없이 robust한 예측을 하려면, 충분한 rating이 확보되어 있어야 함
- new user가 가입할 때 preference keywords를 입력할 수도 있지만, 이는 knowledge-based에 가까운 추천 방식일 수 있음

<br/>

#### 1.3.3 Knowledge-based Recommender Systems
- useful in the context of items are not purchased very often
  - real estate, automobiles, tourism requests, financial services, expensive luxury goods
  - `the cold-start problem`: 추천 제공을 위한 충분한 history data가 없음
  - 또는, 충분한 데이터가 있더라도 이를 통해 유저의 선호를 fully 파악하기 어려울 때 - 특정 브랜드, 측정 모델만을 선호하는 경우

<br/>

##### The types of interface
1. Constraint-Based
   - users specify requirements or constraints

2. Case-based
   - specific cases are specified by the user as targets or anchor points
   - similarity metrics are defined on the item attributes to retrieve similar items to these cases
   - the similarity metrics often carefully defined in a domain-specific way

<br/>

##### The interactivity in knowledge-based recommender systems
1. Conversational systems
   - 유저의 preference는 반복적인 feedback loop를 통해 결정됨
2. Search-based systems
   - preset sequence of questions를 통해 유저의 preference를 결정
3. Navigation-based systems
   - 현재 추천된 아이템에 대해 유저가 change requests를 specify함

<br/>

#### 기타
- Utility-based Recommender Systems
- Demographic Recommender Systems
- Hybrid and Ensemble-Based Recommneder Systems

<br/>

### 1.6 Summary
#### 앞으로 다룰 것들
- 다양한 추천 시스템의 장단점
- different domain-specific scenarios, different types of input information, knowledge-bases
- advanced topics: attack models, group recommender systems, multi-criteria systems, active learning systems
