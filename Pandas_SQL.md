## pandas를 이용하여 SQL 쿼리 수행


```python
import pandas as pd
import numpy as np
```


```python
emp = pd.read_csv('../data/emp.csv')
emp
```




<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>empno</th>
      <th>ename</th>
      <th>job</th>
      <th>mgr</th>
      <th>hiredate</th>
      <th>sal</th>
      <th>comm</th>
      <th>deptno</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>7369</td>
      <td>SMITH</td>
      <td>CLERK</td>
      <td>7902.0</td>
      <td>1980-12-17</td>
      <td>800.0</td>
      <td>NaN</td>
      <td>20</td>
    </tr>
    <tr>
      <th>1</th>
      <td>7499</td>
      <td>ALLEN</td>
      <td>SALESMAN</td>
      <td>7698.0</td>
      <td>1981-02-20</td>
      <td>1600.0</td>
      <td>300.0</td>
      <td>30</td>
    </tr>
    <tr>
      <th>2</th>
      <td>7521</td>
      <td>WARD</td>
      <td>SALESMAN</td>
      <td>7698.0</td>
      <td>1981-02-22</td>
      <td>1250.0</td>
      <td>500.0</td>
      <td>30</td>
    </tr>
    <tr>
      <th>3</th>
      <td>7566</td>
      <td>JONES</td>
      <td>MANAGER</td>
      <td>7839.0</td>
      <td>1981-04-02</td>
      <td>2975.0</td>
      <td>NaN</td>
      <td>20</td>
    </tr>
    <tr>
      <th>4</th>
      <td>7654</td>
      <td>MARTIN</td>
      <td>SALESMAN</td>
      <td>7698.0</td>
      <td>1981-09-28</td>
      <td>1250.0</td>
      <td>1400.0</td>
      <td>30</td>
    </tr>
    <tr>
      <th>5</th>
      <td>7698</td>
      <td>BLAKE</td>
      <td>MANAGER</td>
      <td>7839.0</td>
      <td>1981-05-01</td>
      <td>2850.0</td>
      <td>NaN</td>
      <td>30</td>
    </tr>
    <tr>
      <th>6</th>
      <td>7782</td>
      <td>CLARK</td>
      <td>MANAGER</td>
      <td>7839.0</td>
      <td>1981-06-09</td>
      <td>2450.0</td>
      <td>NaN</td>
      <td>10</td>
    </tr>
    <tr>
      <th>7</th>
      <td>7788</td>
      <td>SCOTT</td>
      <td>ANALYST</td>
      <td>7566.0</td>
      <td>1987-04-19</td>
      <td>3000.0</td>
      <td>NaN</td>
      <td>20</td>
    </tr>
    <tr>
      <th>8</th>
      <td>7839</td>
      <td>KING</td>
      <td>PRESIDENT</td>
      <td>NaN</td>
      <td>1981-11-17</td>
      <td>5000.0</td>
      <td>NaN</td>
      <td>10</td>
    </tr>
    <tr>
      <th>9</th>
      <td>7844</td>
      <td>TURNER</td>
      <td>SALESMAN</td>
      <td>7698.0</td>
      <td>1981-09-08</td>
      <td>1500.0</td>
      <td>0.0</td>
      <td>30</td>
    </tr>
    <tr>
      <th>10</th>
      <td>7876</td>
      <td>ADAMS</td>
      <td>CLERK</td>
      <td>7788.0</td>
      <td>1987-05-23</td>
      <td>1100.0</td>
      <td>NaN</td>
      <td>20</td>
    </tr>
    <tr>
      <th>11</th>
      <td>7900</td>
      <td>JAMES</td>
      <td>CLERK</td>
      <td>7698.0</td>
      <td>1981-12-03</td>
      <td>950.0</td>
      <td>NaN</td>
      <td>30</td>
    </tr>
    <tr>
      <th>12</th>
      <td>7902</td>
      <td>FORD</td>
      <td>ANALYST</td>
      <td>7566.0</td>
      <td>1981-12-03</td>
      <td>3000.0</td>
      <td>NaN</td>
      <td>20</td>
    </tr>
    <tr>
      <th>13</th>
      <td>7934</td>
      <td>MILLER</td>
      <td>CLERK</td>
      <td>7782.0</td>
      <td>1982-01-23</td>
      <td>1300.0</td>
      <td>NaN</td>
      <td>10</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 1. 전체 사원의 이름과 사원번호를 출력하라.
emp[['ename', 'empno']]
```




<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>ename</th>
      <th>empno</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>SMITH</td>
      <td>7369</td>
    </tr>
    <tr>
      <th>1</th>
      <td>ALLEN</td>
      <td>7499</td>
    </tr>
    <tr>
      <th>2</th>
      <td>WARD</td>
      <td>7521</td>
    </tr>
    <tr>
      <th>3</th>
      <td>JONES</td>
      <td>7566</td>
    </tr>
    <tr>
      <th>4</th>
      <td>MARTIN</td>
      <td>7654</td>
    </tr>
    <tr>
      <th>5</th>
      <td>BLAKE</td>
      <td>7698</td>
    </tr>
    <tr>
      <th>6</th>
      <td>CLARK</td>
      <td>7782</td>
    </tr>
    <tr>
      <th>7</th>
      <td>SCOTT</td>
      <td>7788</td>
    </tr>
    <tr>
      <th>8</th>
      <td>KING</td>
      <td>7839</td>
    </tr>
    <tr>
      <th>9</th>
      <td>TURNER</td>
      <td>7844</td>
    </tr>
    <tr>
      <th>10</th>
      <td>ADAMS</td>
      <td>7876</td>
    </tr>
    <tr>
      <th>11</th>
      <td>JAMES</td>
      <td>7900</td>
    </tr>
    <tr>
      <th>12</th>
      <td>FORD</td>
      <td>7902</td>
    </tr>
    <tr>
      <th>13</th>
      <td>MILLER</td>
      <td>7934</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 2. 전체 사원의 이름, 고용일, 매니저, 부서번호를 출력하라.
emp[['ename', 'hiredate', 'mgr', 'deptno']]
```




<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>ename</th>
      <th>hiredate</th>
      <th>mgr</th>
      <th>deptno</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>SMITH</td>
      <td>1980-12-17</td>
      <td>7902.0</td>
      <td>20</td>
    </tr>
    <tr>
      <th>1</th>
      <td>ALLEN</td>
      <td>1981-02-20</td>
      <td>7698.0</td>
      <td>30</td>
    </tr>
    <tr>
      <th>2</th>
      <td>WARD</td>
      <td>1981-02-22</td>
      <td>7698.0</td>
      <td>30</td>
    </tr>
    <tr>
      <th>3</th>
      <td>JONES</td>
      <td>1981-04-02</td>
      <td>7839.0</td>
      <td>20</td>
    </tr>
    <tr>
      <th>4</th>
      <td>MARTIN</td>
      <td>1981-09-28</td>
      <td>7698.0</td>
      <td>30</td>
    </tr>
    <tr>
      <th>5</th>
      <td>BLAKE</td>
      <td>1981-05-01</td>
      <td>7839.0</td>
      <td>30</td>
    </tr>
    <tr>
      <th>6</th>
      <td>CLARK</td>
      <td>1981-06-09</td>
      <td>7839.0</td>
      <td>10</td>
    </tr>
    <tr>
      <th>7</th>
      <td>SCOTT</td>
      <td>1987-04-19</td>
      <td>7566.0</td>
      <td>20</td>
    </tr>
    <tr>
      <th>8</th>
      <td>KING</td>
      <td>1981-11-17</td>
      <td>NaN</td>
      <td>10</td>
    </tr>
    <tr>
      <th>9</th>
      <td>TURNER</td>
      <td>1981-09-08</td>
      <td>7698.0</td>
      <td>30</td>
    </tr>
    <tr>
      <th>10</th>
      <td>ADAMS</td>
      <td>1987-05-23</td>
      <td>7788.0</td>
      <td>20</td>
    </tr>
    <tr>
      <th>11</th>
      <td>JAMES</td>
      <td>1981-12-03</td>
      <td>7698.0</td>
      <td>30</td>
    </tr>
    <tr>
      <th>12</th>
      <td>FORD</td>
      <td>1981-12-03</td>
      <td>7566.0</td>
      <td>20</td>
    </tr>
    <tr>
      <th>13</th>
      <td>MILLER</td>
      <td>1982-01-23</td>
      <td>7782.0</td>
      <td>10</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 3. 직업이 'salesman 인 사원의 이름과 직업 봉급을 출력해보자.'
emp[['ename', 'job']][emp['job']=='SALESMAN']
```




<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>ename</th>
      <th>job</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>ALLEN</td>
      <td>SALESMAN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>WARD</td>
      <td>SALESMAN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>MARTIN</td>
      <td>SALESMAN</td>
    </tr>
    <tr>
      <th>9</th>
      <td>TURNER</td>
      <td>SALESMAN</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 4. 월급이 3000 이상이 사원의 이름과 봉급을 출력하자.
emp[['ename', 'sal']][emp['sal'] >= 3000]
```




<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>ename</th>
      <th>sal</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>7</th>
      <td>SCOTT</td>
      <td>3000.0</td>
    </tr>
    <tr>
      <th>8</th>
      <td>KING</td>
      <td>5000.0</td>
    </tr>
    <tr>
      <th>12</th>
      <td>FORD</td>
      <td>3000.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 5. 사원의 이름과 월급을 출력하되 1000 이상 3000이하
emp[['ename', 'sal']][(emp['sal'] >=1000) & (emp['sal'] <=3000)]
```




<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>ename</th>
      <th>sal</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>ALLEN</td>
      <td>1600.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>WARD</td>
      <td>1250.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>JONES</td>
      <td>2975.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>MARTIN</td>
      <td>1250.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>BLAKE</td>
      <td>2850.0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>CLARK</td>
      <td>2450.0</td>
    </tr>
    <tr>
      <th>7</th>
      <td>SCOTT</td>
      <td>3000.0</td>
    </tr>
    <tr>
      <th>9</th>
      <td>TURNER</td>
      <td>1500.0</td>
    </tr>
    <tr>
      <th>10</th>
      <td>ADAMS</td>
      <td>1100.0</td>
    </tr>
    <tr>
      <th>12</th>
      <td>FORD</td>
      <td>3000.0</td>
    </tr>
    <tr>
      <th>13</th>
      <td>MILLER</td>
      <td>1300.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
emp[['ename', 'sal']][emp['sal'].between(1000, 3000)]
```




<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>ename</th>
      <th>sal</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>ALLEN</td>
      <td>1600.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>WARD</td>
      <td>1250.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>JONES</td>
      <td>2975.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>MARTIN</td>
      <td>1250.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>BLAKE</td>
      <td>2850.0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>CLARK</td>
      <td>2450.0</td>
    </tr>
    <tr>
      <th>7</th>
      <td>SCOTT</td>
      <td>3000.0</td>
    </tr>
    <tr>
      <th>9</th>
      <td>TURNER</td>
      <td>1500.0</td>
    </tr>
    <tr>
      <th>10</th>
      <td>ADAMS</td>
      <td>1100.0</td>
    </tr>
    <tr>
      <th>12</th>
      <td>FORD</td>
      <td>3000.0</td>
    </tr>
    <tr>
      <th>13</th>
      <td>MILLER</td>
      <td>1300.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 6. 사원의 이름과 월급을 출력하되 1000 이상 3000이하가 아닌 목록을 출력하자.
```


```python
emp[['ename', 'sal']][~emp['sal'].between(1000, 3000)]
```




<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>ename</th>
      <th>sal</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>SMITH</td>
      <td>800.0</td>
    </tr>
    <tr>
      <th>8</th>
      <td>KING</td>
      <td>5000.0</td>
    </tr>
    <tr>
      <th>11</th>
      <td>JAMES</td>
      <td>950.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 7. 직업이 analyst, salesman인 사원의 이름과 직업을 출력하자.

#   데이터 베이스   vs   pandas
# between ..and..      / Series.between()
# in                   / isin()
# is null              / isnull()
# like                 / apply() 

emp[['ename', 'job']][(emp['job']=='ANALYST')|(emp['job']=='SALESMAN')]
```




<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>ename</th>
      <th>job</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>ALLEN</td>
      <td>SALESMAN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>WARD</td>
      <td>SALESMAN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>MARTIN</td>
      <td>SALESMAN</td>
    </tr>
    <tr>
      <th>7</th>
      <td>SCOTT</td>
      <td>ANALYST</td>
    </tr>
    <tr>
      <th>9</th>
      <td>TURNER</td>
      <td>SALESMAN</td>
    </tr>
    <tr>
      <th>12</th>
      <td>FORD</td>
      <td>ANALYST</td>
    </tr>
  </tbody>
</table>
</div>




```python
emp[['ename', 'job']][emp['job'].isin(['ANALYST', 'SALESMAN'])]
```




<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>ename</th>
      <th>job</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>ALLEN</td>
      <td>SALESMAN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>WARD</td>
      <td>SALESMAN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>MARTIN</td>
      <td>SALESMAN</td>
    </tr>
    <tr>
      <th>7</th>
      <td>SCOTT</td>
      <td>ANALYST</td>
    </tr>
    <tr>
      <th>9</th>
      <td>TURNER</td>
      <td>SALESMAN</td>
    </tr>
    <tr>
      <th>12</th>
      <td>FORD</td>
      <td>ANALYST</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 8. 커미션이 책정되지 않은 사원의 이름과 봉급 커미션을 출력하자.
emp[['ename', 'sal', 'comm']][emp['comm'].isnull()]
```




<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>ename</th>
      <th>sal</th>
      <th>comm</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>SMITH</td>
      <td>800.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>JONES</td>
      <td>2975.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>5</th>
      <td>BLAKE</td>
      <td>2850.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>6</th>
      <td>CLARK</td>
      <td>2450.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>7</th>
      <td>SCOTT</td>
      <td>3000.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>8</th>
      <td>KING</td>
      <td>5000.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>10</th>
      <td>ADAMS</td>
      <td>1100.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>11</th>
      <td>JAMES</td>
      <td>950.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>12</th>
      <td>FORD</td>
      <td>3000.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>13</th>
      <td>MILLER</td>
      <td>1300.0</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 9. 사원의 이름이 scott 인 사람의 이름과 봉급을 출력
emp[['ename', 'sal']][emp['ename'] == 'SCOTT']
```




<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>ename</th>
      <th>sal</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>7</th>
      <td>SCOTT</td>
      <td>3000.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 10. 이름만 추출해서 첫 글자와 마지막 글자만 출력해보자.
for i in emp['ename']:
    print(i[0], i[-1])
```

    S H
    A N
    W D
    J S
    M N
    B E
    C K
    S T
    K G
    T R
    A S
    J S
    F D
    M R
    


```python
# 11. 이름만 추출해서 마지막 글자가 t로 끝나는거 추출
for i in emp['ename']:
    if i[-1] == 'T':
        print(i)       
```

    SCOTT
    


```python
# 12. str + str / str + int 결합을 python 코드로 한다면?
# 시리즈 + 시리즈로 하나의 시리즈를 새로 만들고 싶을 때
# ename + sal 을 이용하여 하나의 시리즈를 만들어라.

for i, j in zip(emp['ename'], emp['sal']):
    print(i + ' : ' + str(j))
```

    SMITH : 800.0
    ALLEN : 1600.0
    WARD : 1250.0
    JONES : 2975.0
    MARTIN : 1250.0
    BLAKE : 2850.0
    CLARK : 2450.0
    SCOTT : 3000.0
    KING : 5000.0
    TURNER : 1500.0
    ADAMS : 1100.0
    JAMES : 950.0
    FORD : 3000.0
    MILLER : 1300.0
    
