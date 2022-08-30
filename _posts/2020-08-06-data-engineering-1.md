---
layout: post
title: "데이터 분석 전과정, 데이터 파이프라인, 데이터 엔지니어링"
date: 2020-08-06
use_math: true
categories:
  - data-science
tags:
  - data-engineering
  - data-science
permalink: /:categories/:title/
---

<!-- {% include adsense.html %} -->

#### 데이터 기반 가설 검증 단계
- 문제 정의 - 데이터 분석 - 가설 수립 - 실험 및 테스팅 - 최적화
- **A/B Test**
  - 두 버전을 비교하여 어떤 버전이 효과적인지 판단하는 분석 방법
  - 일반적으로 A를 현재 버전, B를 수정된 버전으로 설정
  - 사용자 행동에 영향을 줄 수 있는 하나의 변형을 제외하면 나머진 동일하게 유지

<br/>

#### 데이터 분석 전과정
1. **데이터 수집**
   1. 인터넷 - Web에서 원하는 데이터 수집 (크롤링)
   2. 데이터베이스 (SQL, NoSQL) - 데이터 저장 및 핸들링
      - SQL, MySQL, HIVE 등에서 command를 통해 데이터셋 만듦
   3. Open API - 일종의 함수, 원하는 데이터 가져올 수 있음
   4. 파일
2. **데이터 구조화**
   1. `JSON` (Java Script Object Notation)
      - similar to Python's Dictionary
   2. `CSV`
   3. `XML`
   4. Plain text
3. **데이터 전처리**
4. **데이터 분석**
   - 통계학, 머신러닝 활용
5. **데이터 시각화 / 서비스 개발**

<br/>

#### 데이터 엔지니어링
- 데이터 수집, 추출, 정제하는 데이터 파이프라인을 구축 및 관리하는 작업

<br/>

#### 수집할 수 있는 데이터 예시
* Business data
  - Facebook
    - 유저 경험이 중요한 비즈니스, 처음부터 데이터 시스템 구축이 성공의 열쇠
    - 유저 정보: UserID, LastLogin
    - 컨텐츠 정보: ContentID, ContentType, Categories
    - 유저 액션: Impression(어떤 컨텐츠를 노출?)/Click, Position in Feed, Comment, Like, etc.
  - E-commerce
    - 유저 경험보다는, 마케팅 채널별 비교, CRM 데이터, 각종 물류 데이터

<br/>

#### 데이터 아키텍처 구축시 유의 사항
* 비용 대비 비즈니스 임팩트가 가장 높은 데이터 확보
* 특정 기술, 솔루션에 얽매여있지 않고 새로운 테크를 빠르게 적용할 수 있는 아키텍처를 만들어야 함
* Real time data 핸들링이 가능한 시스템
* Security 유의
* Self-service 환경 구축
  - BI Tools 등 확장성
* API
  - 다양한 플랫폼, 소프트웨어들을 API를 통해 데이터를 주고 받을 수 있는 환경을 구축
* Serverless Framework
  - Triggered by requests, database events, queuing services
  - Pay as you use
  - Form of functions
  - third party 앱 및 다양한 API를 통해 데이터를 수집, 정제하는데 유용
  - e.g.) AWS

<br/>

#### 데이터 파이프라인
- 데이터를 한 장소에서 다른 장소로 옮기는 것
  - API -> Database
  - Database -> Database
  - Database -> BI Tools
- 다양한 데이터 소스로부터 많은 데이터를 생성, 저장
- 실시간 혹은 높은 수준의 데이터 분석이 필요한 비즈니스 모델
- 클라우드 환경으로 데이터 저장
- 데이터 사일로
  - marketing, accounting, sales, operation 등 각 영역의 데이터가 서로 고립되어 있는 경우
- 데이터 파이프라인 구축시 고려사항
  - Scalability, Stability, Security

<br/>

#### 데이터 프로세싱 자동화
  - 필요한 데이터를 추출, 수집, 정제하는 프로세싱을 machine이 운영
  - e.g.) machine scheduling
  - 에러 핸들링 및 모니터
  - 트리거(다음 작업), 스케줄링

<br/>

#### 데이터를 수집하는 목적
1. 데이터 검색
   - 대량의 데이터 중 조건에 맞는 것을 찾고 싶은 경우
2. 데이터 가공
   - 업무 시스템의 일부로서 데이터 처리 결과를 이용하고 싶은 경우
   - 필요한 데이터를 계획적으로 모아 데이터 파이프라인을 설계
   - 시스템 개발 영역 - 자동화가 필수적
3. 데이터 시각화
   - tools: Tableau, D3, QuickSight

<br/>

#### Ad hoc v.s. Automated
- Ad-hoc (애드혹) 분석
  - 분석을 하고 싶을 때만 특정 목적을 갖고 수작업으로 하는 일회성 데이터 분석
  - 데이터 마트를 만들지 않고 데이터 레이크, 데이터 웨어하우스에 직접 연결
    - 복잡한 데이터 분석에서는 먼저 데이터 마트를 구축한 후에 분석, 시각화하는 것이 좋음
- Automated
  - 이벤트, 스케줄 등 트리거를 통해 자동화 시스템 구축
