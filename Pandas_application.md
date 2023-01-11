>> ## 판다스의 활용
***



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
# Q1) select job, max(sal) from emp group by job;
# reset_index() 키워드는 Series(컬럼) 로 출력하는게 아니라 DataFrame(테이블) 으로 출력하는 키워드

result = emp.groupby('job')['sal'].max().reset_index()
print(type(result))
print(result)
```

    <class 'pandas.core.frame.DataFrame'>
             job     sal
    0    ANALYST  3000.0
    1      CLERK  1300.0
    2    MANAGER  2975.0
    3  PRESIDENT  5000.0
    4   SALESMAN  1600.0
    


```python
# Q2) select deptno, sum(sal) from emp where deptno !=20 group by deptno

result = emp.groupby('deptno')['sal'].sum().reset_index()
print(result[['deptno', 'sal']][result['deptno'] != 20])
```

       deptno     sal
    0      10  8750.0
    2      30  9400.0
    


```python
# Q3) 부서번호, 부서별 평균월급을 구해보자.

result = emp.groupby('deptno')['sal'].mean().reset_index()
print(result)
print(type(result))
```

       deptno          sal
    0      10  2916.666667
    1      20  2175.000000
    2      30  1566.666667
    <class 'pandas.core.frame.DataFrame'>
    


```python
# Q4) Q3에서  평균 월급을 출력할 때 정수부분만 출력하고 싶다. (astype(데이터형))

result = emp.groupby('deptno')['sal'].mean().reset_index().astype(int)
print(result)

```

       deptno   sal
    0      10  2916
    1      20  2175
    2      30  1566
    


```python
# Q5) 부서 위치, 부서별 월급의 합을 구해보자.

emp = pd.read_csv('../data/emp.csv')
dept = pd.read_csv('../data/dept.csv')
result = pd.merge(emp, dept, on = 'deptno')
result02 = result.groupby('loc')['sal'].sum().reset_index()
print(result02)
```

            loc      sal
    0   CHICAGO   9400.0
    1    DALLAS  10875.0
    2  NEW YORK   8750.0


***


>> ## Merge(Table 1, Table 2, how = , on =   )

- how ='inner' : emp 와 dept 데이터 프레임에 공통적으로 존재하는 교집합일 경우에만 추출하겠다.
        
- how ='outer' : 열의 데이터가 양쪽 데이터 프레임에 공통적으로 존재하는 교집합이 아니어도 추출하겠다.
                           
- how ='left'  :   왼쪽 데이터 프레임의 키열에 속하는 데이터값을 기준으로 병합하겠다.
        
- how = 'right' :  오른쪽 데이터 프레임의 키열에 속하는 데이터 값을 기준으로 병합하겠다.



```python
# Q6) select loc, sum(sal)
# from emp outer right join dept using (deptno)
# group by loc;

result = pd.merge(emp, dept, how = 'right', on = 'deptno')
result02 = result.groupby('loc')['sal'].sum().reset_index()
print(result02)
```

            loc      sal
    0    BOSTON      0.0
    1   CHICAGO   9400.0
    2    DALLAS  10875.0
    3  NEW YORK   8750.0
    


```python
# Q7) csv 모듈을 이용해서 emp.csv를 읽어오자.

import csv
file = open('../data/emp.csv')
emp_res = csv.reader(file)
for m_list in emp_res:
    print(m_list)
```

    ['empno', 'ename', 'job', 'mgr', 'hiredate', 'sal', 'comm', 'deptno']
    ['7369', 'SMITH', 'CLERK', '7902', '1980-12-17', '800.00', 'NULL', '20']
    ['7499', 'ALLEN', 'SALESMAN', '7698', '1981-02-20', '1600.00', '300.00', '30']
    ['7521', 'WARD', 'SALESMAN', '7698', '1981-02-22', '1250.00', '500.00', '30']
    ['7566', 'JONES', 'MANAGER', '7839', '1981-04-02', '2975.00', 'NULL', '20']
    ['7654', 'MARTIN', 'SALESMAN', '7698', '1981-09-28', '1250.00', '1400.00', '30']
    ['7698', 'BLAKE', 'MANAGER', '7839', '1981-05-01', '2850.00', 'NULL', '30']
    ['7782', 'CLARK', 'MANAGER', '7839', '1981-06-09', '2450.00', 'NULL', '10']
    ['7788', 'SCOTT', 'ANALYST', '7566', '1987-04-19', '3000.00', 'NULL', '20']
    ['7839', 'KING', 'PRESIDENT', 'NULL', '1981-11-17', '5000.00', 'NULL', '10']
    ['7844', 'TURNER', 'SALESMAN', '7698', '1981-09-08', '1500.00', '0.00', '30']
    ['7876', 'ADAMS', 'CLERK', '7788', '1987-05-23', '1100.00', 'NULL', '20']
    ['7900', 'JAMES', 'CLERK', '7698', '1981-12-03', '950.00', 'NULL', '30']
    ['7902', 'FORD', 'ANALYST', '7566', '1981-12-03', '3000.00', 'NULL', '20']
    ['7934', 'MILLER', 'CLERK', '7782', '1982-01-23', '1300.00', 'NULL', '10']
    


```python
# Q8) emp_res 객체를 통해서 이름과 봉급을 구하자. 단 봉급은 월급 * 11.2 로 구하자.
```


```python
file = open('../data/emp02.csv')
emp_res = csv.reader(file)
for m_list in emp_res:
    r = float(m_list[5])*11.2
    print(m_list[1], round(r))
```

    SMITH 8960
    ALLEN 17920
    WARD 14000
    JONES 33320
    MARTIN 14000
    BLAKE 31920
    CLARK 27440
    SCOTT 33600
    KING 56000
    TURNER 16800
    ADAMS 12320
    JAMES 10640
    FORD 33600
    MILLER 14560
    


```python
# Q8) emp_res에서 직업이 salesman인 사원의 이름과 직업을 출력해보자.

file = open('../data/emp02.csv')
emp_res = csv.reader(file)
for m_list in emp_res:
    if m_list[2] == 'SALESMAN':
        print(m_list[1], m_list[2])
```

    ALLEN SALESMAN
    WARD SALESMAN
    MARTIN SALESMAN
    TURNER SALESMAN

*** 

>> ## 결측치 (NaN = Not a Number)
- isnull()


```python
# Q9) emp.csv 를 읽어서 결측치를 확인하자.  <<중요!!>
#(결측지 NaN = Not a Number)

emp = pd.read_csv('../data/emp.csv')
print(emp[['ename', 'comm']])
```

         ename    comm
    0    SMITH     NaN
    1    ALLEN   300.0
    2     WARD   500.0
    3    JONES     NaN
    4   MARTIN  1400.0
    5    BLAKE     NaN
    6    CLARK     NaN
    7    SCOTT     NaN
    8     KING     NaN
    9   TURNER     0.0
    10   ADAMS     NaN
    11   JAMES     NaN
    12    FORD     NaN
    13  MILLER     NaN
    


```python
# Q10) 커미션 결측치를 확인 해보자.

print(emp[['ename', 'comm']] [emp['comm'].isnull()])
```

         ename  comm
    0    SMITH   NaN
    3    JONES   NaN
    5    BLAKE   NaN
    6    CLARK   NaN
    7    SCOTT   NaN
    8     KING   NaN
    10   ADAMS   NaN
    11   JAMES   NaN
    12    FORD   NaN
    13  MILLER   NaN
    


```python
# Q11) 커미션 결측치가 아닌 정보를 확인 해보자. ('~' 틸드를 통해 not 조건)

print(emp[['ename', 'comm']] [~emp['comm'].isnull()])
```

        ename    comm
    1   ALLEN   300.0
    2    WARD   500.0
    4  MARTIN  1400.0
    9  TURNER     0.0
    


```python
# Q12) 전체 emp.csv의 결측치를 확인

print(emp.isnull()) 
```

        empno  ename    job    mgr  hiredate    sal   comm  deptno
    0   False  False  False  False     False  False   True   False
    1   False  False  False  False     False  False  False   False
    2   False  False  False  False     False  False  False   False
    3   False  False  False  False     False  False   True   False
    4   False  False  False  False     False  False  False   False
    5   False  False  False  False     False  False   True   False
    6   False  False  False  False     False  False   True   False
    7   False  False  False  False     False  False   True   False
    8   False  False  False   True     False  False   True   False
    9   False  False  False  False     False  False  False   False
    10  False  False  False  False     False  False   True   False
    11  False  False  False  False     False  False   True   False
    12  False  False  False  False     False  False   True   False
    13  False  False  False  False     False  False   True   False
    


```python
# Q13) 전체 emp.csv의 결측치의 합계를 다시 확인

print(emp.isnull().sum())
```

    empno        0
    ename        0
    job          0
    mgr          1
    hiredate     0
    sal          0
    comm        10
    deptno       0
    dtype: int64
    
***

>> ## 파생데이터 생성 = 파생변수
- 기존의 데이터를 가지고 가공해서 만든 새로운 데이터의 컬럼


```python
# Q14) emp에 있는 sal 을 sal02라는 컬럼을 생성해서 추가하자.

emp = pd.read_csv('../data/emp.csv')
emp['sal02'] = emp['sal']
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
      <th>sal02</th>
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
      <td>800.0</td>
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
      <td>1600.0</td>
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
      <td>1250.0</td>
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
      <td>2975.0</td>
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
      <td>1250.0</td>
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
      <td>2850.0</td>
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
      <td>2450.0</td>
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
      <td>3000.0</td>
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
      <td>5000.0</td>
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
      <td>1500.0</td>
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
      <td>1100.0</td>
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
      <td>950.0</td>
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
      <td>3000.0</td>
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
      <td>1300.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Q15) 이름과 부서 위치를 출력해보자. 조인 확인 후 `result loc`를 emp테이블에 추가해서 파생변수를 만들자.

emp = pd.read_csv('../data/emp.csv')
dept = pd.read_csv('../data/dept.csv')
result = pd.merge(emp, dept, how = 'inner', on = 'deptno')
emp['loc'] = result['loc']
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
      <th>loc</th>
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
      <td>DALLAS</td>
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
      <td>DALLAS</td>
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
      <td>DALLAS</td>
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
      <td>DALLAS</td>
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
      <td>DALLAS</td>
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
      <td>CHICAGO</td>
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
      <td>CHICAGO</td>
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
      <td>CHICAGO</td>
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
      <td>CHICAGO</td>
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
      <td>CHICAGO</td>
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
      <td>CHICAGO</td>
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
      <td>NEW YORK</td>
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
      <td>NEW YORK</td>
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
      <td>NEW YORK</td>
    </tr>
  </tbody>
</table>
</div>

