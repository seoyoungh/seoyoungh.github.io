---
layout: post
title: "Pandas 기초 syntax"
date: 2020-08-05
use_math: true
categories:
  - data-science
tags:
  - pandas
  - machine-learning
  - data-analysis
permalink: /:categories/:title/
---

<!-- {% include adsense.html %} -->

#### Pandas Data Type (dtype)
파이썬의 데이터 타입과는 다른 pandas의 data type.

- `object`: string
- `int64`: int
- `float64`: float
- `bool`: boolean
- `datetime64`: 날짜/시간
- `timedelta[ns]`: 두 datatime64 간의 차

<br/>

#### Pandas Series & Dataframe
- series: 하나의 column
- dataframe: table 형태, 여러개의 series
  - column name이 결국 열의 index
  - df의 특정 column의 data type은 series

<br/>

#### Pandas 데이터프레임 읽기
- 구분자는 보통 comma이지만 특수한 경우 데이터에 맞게 지정
- 에러나는 데이터는 보통 제외하고 로드

```python
# csv
doc = pd.read_csv("file_name", encoding='utf-8-sig', quotechar=',', error_bad_lines=False)

# excel (특정 sheet 로드시)
doc = pd.read_excel("file_name", sheet_name="sheet_name")
```

<br/>

#### Pandas 데이터프레임 기본 syntax

```python
df = pd.DataFrame({
    "미국": [2.1, 2.2, 2.3],
    "한국": [0.4, 0.5, 0.45],
    "중국": [10, 13, 15]},
    index = [2000, 2010, 2020]
)

df.columns # Index(['미국', '한국', '중국'], dtype='object')
df.values # array([[ 2.1 ,  0.4 , 10.  ],
          #        [ 2.2 ,  0.5 , 13.  ],
          #        [ 2.3 ,  0.45, 15.  ]])

# index  
df = df.set_index('년도') # 인덱스 이름을 년도로 설정
df.index.name = '연도' # 연도로 수정
df.index.name # '연도'
df = df.reset_index('연도') # 인덱스를 컬럼으로 변경
df = df.set_index('연도') # 다시 인덱스로 설정

# 특정 열 찾기
df.loc[2000] # column name으로 열 찾기
df.iloc[0] # column index로 열 찾기

# column 추가
df['일본'] = [1, 2, 3]
# column 삭제
del df['일본']
# row 삭제
df.drop([2020]) # row 삭제

# 필요한 column만 추출
df2 = df[['중국', '한국']]
df2 = df[['중국', '한국']].copy() # 필요한 컬럼만 새 데이터프레임으로 복사

# 필요한 row 추출
doc_us = doc[doc['Country_Region'] == 'US']
```

<br/>

#### Series 관련 syntax

```python
countries = doc['Country_Region'] # 해당 column series만 추출
countries.size # 사이즈
countries.count() # 데이터 없는 경우 제외한 사이즈
countries.unique() # 유일한 값 리턴
countries.value_counts() # 데이터가 없는 경우 제외한 각 값의 개수
```

<br/>

#### 결측치 처리

```python
doc.isnull().sum() # 각 column의 결측치의 개수
doc = doc.dropna() # 하나라도 결측치가 있으면 해당 row 삭제
doc = doc.dropna(subset=['Confirmed']) # 해당 col에 결측치가 있으면 해당 row 삭제
doc = doc.fillna(0) # 0으로 결측치를 대체
nan_data = {'Confirmed': 0, 'Recovered': 0}
doc = doc.fillna(nan_data) # 위에서 지정한 col에 대해 지정한 value로 결측치 대체
```

<br/>

#### 특정 키로 데이터 합치기
- `groupby()`: 문자열 value를 갖는 row는 없어짐

```python
doc = doc.groupby('Country_Region').sum() # 같은 키값을 갖는 항목들의 데이터를 합쳐줌
doc = doc.groupby('Country_Region').mean() # 같은 키값을 갖는 항목들의 평균으로 합침
doc.index # groupby()의 기준이 된 key로 index가 변경됨
```

<br/>

#### 컬럼 타입 변경

```python
doc = doc[['Country/Region', 'Confirmed']] # 필요한 컬럼만 선택하기
doc = doc.dropna(subset=['Confirmed'])     # 특정 컬럼에 없는 데이터 삭제하기
doc = doc.astype({'Confirmed': 'int64'})   # 특정 컬럼의 데이터 타입 변경하기
```

<br/>

#### 컬럼 이름 변경

```python
doc = doc[['Country/Region', 'Confirmed']]
doc.columns = ['Country_Region', 'Confirmed']
```

```python
# 중간에 컬럼명이 바뀌는 경우 -> try except 구문 활용
try:
    doc = doc[['Province_State', 'Country_Region', 'Confirmed']]
except:
    doc = doc[['Province/State', 'Country/Region', 'Confirmed']]
    doc.columns = ['Province_State', 'Country_Region', 'Confirmed']
```

<br/>

#### 데이터프레임 중복 행 제거

```python
doc.duplicated() # 해당 행이 중복행인지 boolean type으로 리턴
doc[doc.duplicated()] # 중복된 행만 확인

# 특정 행 기준 중복 제거
# 처음 or 마지막 행 중 어느 것을 남길지: keep = 'first'(defult) or 'last'
doc = doc.drop_duplicates(subset='Country_Region', keep='last')
```

<br/>

#### 데이터프레임 합치기
- `concat`: 단순히 위아래/좌우로 붙이는 것
  - `axis`: 0 (위아래) or 1 (좌우)

```python
pd.concat([df1, df2]) # axis=0(default): 위아래로 합침
doc = pd.concat([df1, df2], axis=1) # axis=1: 좌우로 합침
```

- `merge`: 동일한 이름의 컬럼을 기준으로 합침 (SQL의 JOIN)
  - `on`: 기준 컬럼명 명시 e.g.) id
  - `how`: 결합 방법 (SQL과 동일)
    1. inner: 내부 조인 **(default)**
       - 기준 컬럼 값이 동일한 row를 찾고, 해당 row만 가져오기
       - 기준 컬럼 값이 동일하지 않은 것은 제거
    2. outer: 외부 조인
       - 기준 컬럼 값이 동일하지 않아도 다 가져오고, 데이터가 없는 값은 `Nan`
    3. left: 왼쪽 우선 외부 조인
       - 왼쪽 데이터프레임의 행을 다 가져옴
       - 오른쪽에서는 기준 컬럼 값이 동일한 row만 가져오고, 데이터가 없는 값은 `Nan`
    4. right: 오른 쪽 우선 외부 조인
       - 오른쪽 데이터프레임의 행을 다 가져옴
       - 왼쪽에서는 기준 컬럼 값이 동일한 row만 가져오고, 데이터가 없는 값은 `Nan`
  - index를 기준 컬럼으로 할 수도 있음

```python
pd.merge(df1, df2) # 기준 컬럼을 명시하지 않아도 동일한 이름의 컬럼을 기준으로 병함함
pd.merge(df1, df2, on='id') # 기준 컬럼 명시
pd.merge(df1, df2, on='id', how='outer') # 결합 방법 명시

# index를 기준으로 병합하기
df1 = df1.set_index('id') # id column을 index로 설정
df2 = df2.set_index('id')
pd.merge(df1, df2, how='outer', left_index=True, right_index=True)
```

<br/>

#### apply 함수
- `df.apply(func, axis=0)`
  - `func`: 값에 적용하고자 하는 function
  - `axis`: 0은 coulmn에 해당 함수 적용, 1은 row에 적용

```python
# col A 값에 2를 더한 새로운 column B 생성 (series)
df['B'] = df['A'].apply(lambda x: x + 2)
# col A 값 + col B 값 = 새로운 column C 생성 (dataframe)
df['C'] = df.apply(lambda x: x.A + x.B, axis=1)
```

```python
df = pd.DataFrame({
    '영어': [60, 70],
    '수학': [100, 50]
}, index = ['Dave', 'David'])

# 함수로 custom function 정의
def func(df_data):
  df_data['영어'] = 80
  return df_data

# row에 적용하므로 axis=1
df_func = df.apply(func, axis=1)
```
