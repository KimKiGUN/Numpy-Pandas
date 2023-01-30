>> ## DataFrame
***


### 데이터프레임

외부파일을 데이터 프레임으로 변환 -> 데이터프레임을 외부파일로 변환

- read_* 함수사용 = 데이터프레임으로 변환해서 가져오기 ex(pd.read_csv('파일명'))
- to_* 함수사용 = 데이터프레임을 csv 파일로 내보내기
ex(pd.to_csv('파일명'))

리스트로 데이터 프레임 만들기

- DataFrame([list1], [list2])- 리스트 안에 리스트 형태로 인수를 전달(2차원 리스트 형태로 전달)

- 각 list는 한 행으로 구성됨
- 행의 원소 개수가 다르면 None 값으로 저장
- index 인수값이 없으면 기본 인덱스(위치 인덱스)가 생성됨


```python
import pandas as pd
import numpy as np
```


```python
df = pd.DataFrame([['a','b','c'],['a','a','g'],['a','a']])
df
```




<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0</th>
      <th>1</th>
      <th>2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>a</td>
      <td>b</td>
      <td>c</td>
    </tr>
    <tr>
      <th>1</th>
      <td>a</td>
      <td>a</td>
      <td>g</td>
    </tr>
    <tr>
      <th>2</th>
      <td>a</td>
      <td>a</td>
      <td>None</td>
    </tr>
  </tbody>
</table>
</div>



딕셔너리로 데이터프레임 생성
- dict의 key -> column name


```python
# 열 데이터를 dict로 작성하는 것이 일반적임
# 열방향 인덱스(dict의 key), 행방향 인덱스(자동생성 숫자)
df1 = pd.DataFrame(
{
    'A' : [90, 80, 70],
    'B' : [85, 98, 75],
    'C' : [88, 99, 77],
    'D' : [87, 89, 86]
}, index = [1, 2, 3] #행 인덱스
)
df1

# 딕셔너리의 key는 columnname, index = 인수는 rowname
```




<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>90</td>
      <td>85</td>
      <td>88</td>
      <td>87</td>
    </tr>
    <tr>
      <th>2</th>
      <td>80</td>
      <td>98</td>
      <td>99</td>
      <td>89</td>
    </tr>
    <tr>
      <th>3</th>
      <td>70</td>
      <td>75</td>
      <td>77</td>
      <td>86</td>
    </tr>
  </tbody>
</table>
</div>




```python
data = {
    '2015' : [9904312, 3448737, 2890451, 2466052],
    '2010' : [9631482, 3393191, 2632035, 2000002],
    '2005' : [9762546, 3512547, 2517680, 2456016],
    '2000' : [9853972, 3655437, 2466338, 2473990],
    '지역' : ['수도권', '경상권', '수도권', '경상권'],
    '2010-2015 증가율' : [0.0283, 0.0163, 0.0982, 0.0141]
}

df3 = pd.DataFrame(data)
df3
```




<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>2015</th>
      <th>2010</th>
      <th>2005</th>
      <th>2000</th>
      <th>지역</th>
      <th>2010-2015 증가율</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>9904312</td>
      <td>9631482</td>
      <td>9762546</td>
      <td>9853972</td>
      <td>수도권</td>
      <td>0.0283</td>
    </tr>
    <tr>
      <th>1</th>
      <td>3448737</td>
      <td>3393191</td>
      <td>3512547</td>
      <td>3655437</td>
      <td>경상권</td>
      <td>0.0163</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2890451</td>
      <td>2632035</td>
      <td>2517680</td>
      <td>2466338</td>
      <td>수도권</td>
      <td>0.0982</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2466052</td>
      <td>2000002</td>
      <td>2456016</td>
      <td>2473990</td>
      <td>경상권</td>
      <td>0.0141</td>
    </tr>
  </tbody>
</table>
</div>



위에서 생성된 데이터 프레임은 열의 순서가 보장되지 않고, 각 행의 의미 전달이 어렵다.
- index 파라미터와 columns 파라미터를 사용해서 df의 의미 전달이 쉬워진다.


```python
columns=['지역', '2000', '2005', '2010', '2015', '2010-2015 증가율']
index = ['서울', '부산', '인천', '대구']
df3 = pd.DataFrame(data, index = index, columns = columns)
df3
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>지역</th>
      <th>2000</th>
      <th>2005</th>
      <th>2010</th>
      <th>2015</th>
      <th>2010-2015 증가율</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>서울</th>
      <td>수도권</td>
      <td>9853972</td>
      <td>9762546</td>
      <td>9631482</td>
      <td>9904312</td>
      <td>0.0283</td>
    </tr>
    <tr>
      <th>부산</th>
      <td>경상권</td>
      <td>3655437</td>
      <td>3512547</td>
      <td>3393191</td>
      <td>3448737</td>
      <td>0.0163</td>
    </tr>
    <tr>
      <th>인천</th>
      <td>수도권</td>
      <td>2466338</td>
      <td>2517680</td>
      <td>2632035</td>
      <td>2890451</td>
      <td>0.0982</td>
    </tr>
    <tr>
      <th>대구</th>
      <td>경상권</td>
      <td>2473990</td>
      <td>2456016</td>
      <td>2000002</td>
      <td>2466052</td>
      <td>0.0141</td>
    </tr>
  </tbody>
</table>
</div>



시리즈로 데이터 프레임 생성
- 각 Series의 인덱스 -> columname


```python
a = pd.Series([100, 200, 300], ['a', 'b', 'd'])
b = pd.Series([101, 201, 301], ['a', 'b', 'k'])
c = pd.Series([110, 210, 310], ['a', 'b', 'c'])
```


```python
pd.DataFrame([a,b,c], index= [100, 101, 102])
```




<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>a</th>
      <th>b</th>
      <th>d</th>
      <th>k</th>
      <th>c</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>100</th>
      <td>100.0</td>
      <td>200.0</td>
      <td>300.0</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>101</th>
      <td>101.0</td>
      <td>201.0</td>
      <td>NaN</td>
      <td>301.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>102</th>
      <td>110.0</td>
      <td>210.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>310.0</td>
    </tr>
  </tbody>
</table>
</div>



csv 데이터로부터 Dataframe 생성
- 데이터 분석을 위해, dataframe을 생성하는 가장 일반적인 방법
- 데이터 소스로부터 추출된 csv(comma separated values) 파일로부터 생성
- pandas.read_csv 함수 사용


```python
train_data = pd.read_csv('../data/train.csv')
train_data.head()  # df의 위 5행만 출력
```




<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>PassengerId</th>
      <th>Survived</th>
      <th>Pclass</th>
      <th>Name</th>
      <th>Sex</th>
      <th>Age</th>
      <th>SibSp</th>
      <th>Parch</th>
      <th>Ticket</th>
      <th>Fare</th>
      <th>Cabin</th>
      <th>Embarked</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>0</td>
      <td>3</td>
      <td>Braund, Mr. Owen Harris</td>
      <td>male</td>
      <td>22.0</td>
      <td>1</td>
      <td>0</td>
      <td>A/5 21171</td>
      <td>7.2500</td>
      <td>NaN</td>
      <td>S</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>1</td>
      <td>1</td>
      <td>Cumings, Mrs. John Bradley (Florence Briggs Th...</td>
      <td>female</td>
      <td>38.0</td>
      <td>1</td>
      <td>0</td>
      <td>PC 17599</td>
      <td>71.2833</td>
      <td>C85</td>
      <td>C</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>1</td>
      <td>3</td>
      <td>Heikkinen, Miss. Laina</td>
      <td>female</td>
      <td>26.0</td>
      <td>0</td>
      <td>0</td>
      <td>STON/O2. 3101282</td>
      <td>7.9250</td>
      <td>NaN</td>
      <td>S</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>1</td>
      <td>1</td>
      <td>Futrelle, Mrs. Jacques Heath (Lily May Peel)</td>
      <td>female</td>
      <td>35.0</td>
      <td>1</td>
      <td>0</td>
      <td>113803</td>
      <td>53.1000</td>
      <td>C123</td>
      <td>S</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>0</td>
      <td>3</td>
      <td>Allen, Mr. William Henry</td>
      <td>male</td>
      <td>35.0</td>
      <td>0</td>
      <td>0</td>
      <td>373450</td>
      <td>8.0500</td>
      <td>NaN</td>
      <td>S</td>
    </tr>
  </tbody>
</table>
</div>



read_csv 함수 파라미터
- sep - 각 데이터 값을 구별하기 위한 구분자(separator) 설정
- header : header를 무시할 경우, None 설정
- index_col : index로 사용할 column 설정
- usecols : 실제로 dataframe에 로딩할 column 만 설정


```python
train_data=pd.read_csv('../data/train.csv',
                      index_col = 'PassengerId',
                      usecols = ['PassengerId', 'Survived', 'Name', 'Sex', 'Age'])
```


```python
# df.columns 속성 : df의 컬럼명을 저장하고 있는 속성
train_data.columns
```




    Index(['Survived', 'Name', 'Sex', 'Age'], dtype='object')




```python
train_data.head()
```




<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Survived</th>
      <th>Name</th>
      <th>Sex</th>
      <th>Age</th>
    </tr>
    <tr>
      <th>PassengerId</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>0</td>
      <td>Braund, Mr. Owen Harris</td>
      <td>male</td>
      <td>22.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
      <td>Cumings, Mrs. John Bradley (Florence Briggs Th...</td>
      <td>female</td>
      <td>38.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1</td>
      <td>Heikkinen, Miss. Laina</td>
      <td>female</td>
      <td>26.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1</td>
      <td>Futrelle, Mrs. Jacques Heath (Lily May Peel)</td>
      <td>female</td>
      <td>35.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>0</td>
      <td>Allen, Mr. William Henry</td>
      <td>male</td>
      <td>35.0</td>
    </tr>
  </tbody>
</table>
</div>



인덱스와 컬럼의 이해
1. 인덱스(index)
    - index 속성
    - 각 아이템을 특정할 수 있는 고유의 값을 저장
    - 복잡한 데이터의 경우, 멀티 인덱스로 표현 가능
2. 컬럼(columns)
    - columns 속성
    - 각각의 특성(feature)을 나타냄
    - 복잡한 데이터의 경우, 멀티 컬럼으로 표현 가능


```python
df3
```




<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>지역</th>
      <th>2000</th>
      <th>2005</th>
      <th>2010</th>
      <th>2015</th>
      <th>2010-2015 증가율</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>서울</th>
      <td>수도권</td>
      <td>9853972</td>
      <td>9762546</td>
      <td>9631482</td>
      <td>9904312</td>
      <td>0.0283</td>
    </tr>
    <tr>
      <th>부산</th>
      <td>경상권</td>
      <td>3655437</td>
      <td>3512547</td>
      <td>3393191</td>
      <td>3448737</td>
      <td>0.0163</td>
    </tr>
    <tr>
      <th>인천</th>
      <td>수도권</td>
      <td>2466338</td>
      <td>2517680</td>
      <td>2632035</td>
      <td>2890451</td>
      <td>0.0982</td>
    </tr>
    <tr>
      <th>대구</th>
      <td>경상권</td>
      <td>2473990</td>
      <td>2456016</td>
      <td>2000002</td>
      <td>2466052</td>
      <td>0.0141</td>
    </tr>
  </tbody>
</table>
</div>




```python
# df의 컬럼명(열 인덱스)을 확인 - df.columns 속성
print(df3.columns)
type(df3.columns)
```

    Index(['지역', '2000', '2005', '2010', '2015', '2010-2015 증가율'], dtype='object')
    




    pandas.core.indexes.base.Index




```python
# df의 행 인덱스를 확인 - df.index 속성
print(type(df3.index))
df3.index
```

    <class 'pandas.core.indexes.base.Index'>
    




    Index(['서울', '부산', '인천', '대구'], dtype='object')



행/열 인덱스 이름 설정
- index.name
- columns.name


```python
df3.index.name='도시'
df3.columns.name='특성'
df3
```




<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th>특성</th>
      <th>지역</th>
      <th>2000</th>
      <th>2005</th>
      <th>2010</th>
      <th>2015</th>
      <th>2010-2015 증가율</th>
    </tr>
    <tr>
      <th>도시</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>서울</th>
      <td>수도권</td>
      <td>9853972</td>
      <td>9762546</td>
      <td>9631482</td>
      <td>9904312</td>
      <td>0.0283</td>
    </tr>
    <tr>
      <th>부산</th>
      <td>경상권</td>
      <td>3655437</td>
      <td>3512547</td>
      <td>3393191</td>
      <td>3448737</td>
      <td>0.0163</td>
    </tr>
    <tr>
      <th>인천</th>
      <td>수도권</td>
      <td>2466338</td>
      <td>2517680</td>
      <td>2632035</td>
      <td>2890451</td>
      <td>0.0982</td>
    </tr>
    <tr>
      <th>대구</th>
      <td>경상권</td>
      <td>2473990</td>
      <td>2456016</td>
      <td>2000002</td>
      <td>2466052</td>
      <td>0.0141</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 데이터 프레임내의 데이터만 접근하려면 values 속성을 사용
print(type(df3.values))
df3.values # df의 value는 2차원 ndarray로 나타난다.
```

    <class 'numpy.ndarray'>
    




    array([['수도권', 9853972, 9762546, 9631482, 9904312, 0.0283],
           ['경상권', 3655437, 3512547, 3393191, 3448737, 0.0163],
           ['수도권', 2466338, 2517680, 2632035, 2890451, 0.0982],
           ['경상권', 2473990, 2456016, 2000002, 2466052, 0.0141]], dtype=object)




```python
type(df3.values[0])
df3.values[0]
```




    array(['수도권', 9853972, 9762546, 9631482, 9904312, 0.0283], dtype=object)



dataframe 데이터 파악하기
- shape 속성(row, column)
- describe 함수 : 숫자형 데이터의 통계치 계산
- info 함수 : 데이터타입, 각 아이템의 개수 등 출력


```python
train_data.head()
```




<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Survived</th>
      <th>Name</th>
      <th>Sex</th>
      <th>Age</th>
    </tr>
    <tr>
      <th>PassengerId</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>0</td>
      <td>Braund, Mr. Owen Harris</td>
      <td>male</td>
      <td>22.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
      <td>Cumings, Mrs. John Bradley (Florence Briggs Th...</td>
      <td>female</td>
      <td>38.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1</td>
      <td>Heikkinen, Miss. Laina</td>
      <td>female</td>
      <td>26.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1</td>
      <td>Futrelle, Mrs. Jacques Heath (Lily May Peel)</td>
      <td>female</td>
      <td>35.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>0</td>
      <td>Allen, Mr. William Henry</td>
      <td>male</td>
      <td>35.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
len(train_data) # df의 행 수
print(train_data.size) # df의 값의 개수
train_data.shape # df의 행과 열 수 
```

    3564
    




    (891, 4)




```python
# 데이터의 요약(개요) 정보 반환
train_data.info()
```

    <class 'pandas.core.frame.DataFrame'>
    Int64Index: 891 entries, 1 to 891
    Data columns (total 4 columns):
     #   Column    Non-Null Count  Dtype  
    ---  ------    --------------  -----  
     0   Survived  891 non-null    int64  
     1   Name      891 non-null    object 
     2   Sex       891 non-null    object 
     3   Age       714 non-null    float64
    dtypes: float64(1), int64(1), object(2)
    memory usage: 34.8+ KB
    


```python
train_data.describe()
# 수치형 데이터에 대해서만 기본 통계량을 반환
```




<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Survived</th>
      <th>Age</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>891.000000</td>
      <td>714.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>0.383838</td>
      <td>29.699118</td>
    </tr>
    <tr>
      <th>std</th>
      <td>0.486592</td>
      <td>14.526497</td>
    </tr>
    <tr>
      <th>min</th>
      <td>0.000000</td>
      <td>0.420000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>0.000000</td>
      <td>20.125000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>0.000000</td>
      <td>28.000000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>1.000000</td>
      <td>38.000000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>1.000000</td>
      <td>80.000000</td>
    </tr>
  </tbody>
</table>
</div>



데이터 프레임 전치
- 판다스 테이터 프레임은 전치를 포함해서 Numpy 2차원 배열의 대부분 속성이나 메서드를 지원한다.
- 전치 : 행과 열을 바꾸는 기능
- df.T


```python
df3.T
```




<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th>도시</th>
      <th>서울</th>
      <th>부산</th>
      <th>인천</th>
      <th>대구</th>
    </tr>
    <tr>
      <th>특성</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>지역</th>
      <td>수도권</td>
      <td>경상권</td>
      <td>수도권</td>
      <td>경상권</td>
    </tr>
    <tr>
      <th>2000</th>
      <td>9853972</td>
      <td>3655437</td>
      <td>2466338</td>
      <td>2473990</td>
    </tr>
    <tr>
      <th>2005</th>
      <td>9762546</td>
      <td>3512547</td>
      <td>2517680</td>
      <td>2456016</td>
    </tr>
    <tr>
      <th>2010</th>
      <td>9631482</td>
      <td>3393191</td>
      <td>2632035</td>
      <td>2000002</td>
    </tr>
    <tr>
      <th>2015</th>
      <td>9904312</td>
      <td>3448737</td>
      <td>2890451</td>
      <td>2466052</td>
    </tr>
    <tr>
      <th>2010-2015 증가율</th>
      <td>0.0283</td>
      <td>0.0163</td>
      <td>0.0982</td>
      <td>0.0141</td>
    </tr>
  </tbody>
</table>
</div>




```python
df3.T['서울'].values
df3.T['서울']['2000']
```




    9853972


