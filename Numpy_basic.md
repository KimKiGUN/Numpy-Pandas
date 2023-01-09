>> ## Numpy
- 수식 라이브러리, 수치연산, 배열객체
- 동작 속도가 빠르다.
- 연속적인 메모리 사용한다.
- 한 가지 타입의 데이터만 처리 가능.

***

>> ### 1) np.array로 객체 생성 / np.arange로 객체 생성

```python
import numpy as np
a = np.array([0, 1, 2, 3, 4, 5])

print(a)
print(type(a))
print(a.dtype)
```

`[0 1 2 3 4 5]`

`<class 'numpy.ndarray'>`

`int32`

***

```python
a = np.array([0.0, 1.0, 2.0, 3.0, 4.0, 5.0])

print(a)
print(type(a))
print(a.dtype)
```

`[0. 1. 2. 3. 4. 5.]`

`<class 'numpy.ndarray'>`

`float64`

***

```python
a = np.arange(10)

print(a)
print(type(a))
```
`[0 1 2 3 4 5 6 7 8 9]`

`<class 'numpy.ndarray'>`

***

>> ### 2) 차원(Rank, Dimension)
- 차원 = [ ]의 개수로 확인
- 1차원 shape (x,)
- 2차원 shape (x, y)
- 3차원 shape (x, y, z)
- n차원 shape (x, y, z, ..)

***
#### 1차원 배열의 shape(x, )
```python
a = np.arange(12)
print(a)
print(a.shape)

t = a.shape
print(type(t))
print((a.shape)[0])
```
`[ 0  1  2  3  4  5  6  7  8  9 10 11]`

`(12,)`

`<class 'tuple'>`

`12`

***

#### 2차원 배열의 shape (x, y): 행(row, axis = 0)과 열 (column, axis = 1)

```python
m = np.array([[0, 1, 2],
              [0, 1, 2]])

print(m)
print(m.shape)
print(m.shape[0], m.shape[1])
```
`[[0 1 2]
 [0 1 2]]`

`(2, 3)`

`2 3`

***

#### 3차원 배열의 shape (x, y, z) : (면, 행, 열)

```python
m = np.array([[[0, 1, 2],
               [3, 4, 5]],
              [[0, 1, 2],
               [3, 4, 5]]])
print(m)
print(m.shape)             
print(m.shape[0],m.shape[1], m.shape[2])
```
`[[[0 1 2]
  [3 4 5]]`

 `[[0 1 2]
  [3 4 5]]]`

`(2, 2, 3)`

`2 2 3`

***

>> ### 2) 재배열(reshape)과 슬라이싱

```python
# 2차원 배열 인덱싱, 슬라이싱
a = np.arange(12).reshape(3,4)
print(a)
print(a.shape)
```
`[[ 0  1  2  3]
 [ 4  5  6  7]
 [ 8  9 10 11]]`

`(3, 4)`

***

```python
# a 가진 값 0, 9, 11을 리턴해보자 = 인덱싱
print(a[0,0])
print(a[0][0])   #0

print(a[2,1])
print(a[2][1])   #9

print(a[2, 3])
print(a[2][3])   #11
```
`0`

`0`

`9`

`9`

`11`

`11`

```python
# 슬라이싱

print(a[0])   
print(a[0, :])      #[0번행, 모든 열]

print(a[:, :-1])    #[모든 행, 마지막 열 제외]
print(a[:, 1:])     #[모든 행, 첫번째 열 제외]

print(a[:,:])       #[모든 행, 모든 열]
```
`[0 1 2 3]`

`[0 1 2 3]`

`[[ 0  1  2]
 [ 4  5  6]
 [ 8  9 10]]`

`[[ 1  2  3]
 [ 5  6  7]
 [ 9 10 11]]`

`[[ 0  1  2  3]
 [ 4  5  6  7]
 [ 8  9 10 11]]`

***

```python
# 0행의 모든 데이터를 20으로 변경 후 전체 출력해보자.

a[0,:] = 20            #1
print(a[:,:])          #2
print(a[::2, ::2])     #3



# 1) 0행의 모든 열을 20으로 바꿈
# 2) a 전체출력
# 3) [start : end -1 : step] / [처음부터 모든 행,열을 2간격씩 띄워서 출력]
```
`[[20 20 20 20]
 [ 4  5  6  7]
 [ 8  9 10 11]]`

`[[20 20]
 [ 8 10]]`

 ***

 ```python
 # 슬라이싱을 이용해 요소 전체의 값을 변경해보자.

a[::2, ::3] = 0      #1
print(a[:,:])

a[:,:] = -1          #2
print(a[:,:])        

#1 [0행, 2행 / 0열, 3열] 의 값을 0으로 변경 (꼭지점)
#2 모든 요소를 -1로 변경
```

`[[ 0 20 20  0]
 [ 4  5  6  7]
 [ 0  9 10  0]]`

`[[-1 -1 -1 -1]
 [-1 -1 -1 -1]
 [-1 -1 -1 -1]]`

***
```python
# 3차원 배열 인덱싱 슬라이싱

a = np.arange(12).reshape(2, 2, 3)
print(a, a.shape)

print(a[0][0][0])  
print(a[0, 1, 2])  #1

#1 0번째 면, 1번 행, 2번 열 요소
```
`[[[ 0  1  2]
  [ 3  4  5]]`

 `[[ 6  7  8]
  [ 9 10 11]]]`

 `(2, 2, 3)`

`0`

`5`

***

```python
# 슬라이싱

print(a[:,:,:])

print(a[:,1:,1:])


# 6, 7을 출력해보자.
print(a[1, 0, :2])       #1  1차원 case
print(a[1, :-1, :-1])    #2  2차원 case
print(a[1:,:-1, :2 ])    #3  3차원 case
```
`[[[ 0  1  2]
  [ 3  4  5]]
 [[ 6  7  8]
  [ 9 10 11]]]`

`[[[ 4  5]]
 [[10 11]]]`

`[6 7]`

`[[6 7]]`

`[[[6 7]]]`

***
>> ### 3) 불린 인덱싱
- 조건식을 이용한 인덱싱, 조건 검색 필터를 사용한 추출값
```python
# ndarray 객체 a에서 2보다 큰 값을 배열로 리턴하자.
# 이미지 이상값(noise) 추출해서 변경할 때 자주 사용.
a = np.array([1, 2, 3 ,4, 5, 6])
print(a > 2)
print(a[a > 2])
```

`[False False  True  True  True  True]`

`[3 4 5 6]`

***

```python
a = np.array([1, 2, 3 ,4, 5, 6])
bool_index = np.array([True, False, True, False, True, True])
print(bool_index)
print(a[bool_index])   #1

#1 a 객체 중 True 인 것만 나온다.
```
`[ True False  True False  True  True]`

`[1 3 5 6]`

***

```python
# 연습문제
# 1) 배열 a에서 3이 아닌 요소를 추출
# 2) 2보다 크고 6보다 낮은 요소를 추출
# 3) 짝수만 추출
# 4) 평균보다 작은 값을 추출해보자.

a = np.array([1, 2, 3 ,4, 5, 6])
print(a[a!=3])  #1
print(a[(a>2) & (a<6)])
print(a[a % 2 == 0])
print(a[a < a.mean()], a.mean())
```
`[1 2 4 5 6]`

`[3 4 5]`

`[2 4 6]`
`[1 2 3]`
`3.5`

***

>> ### 4) 배열의 형상 다루기 
- reshape(), flatten()(편형화), transpose()(전치)
```python
# flatten() : 다차원 배열을 1차원으로 만든다

a = np.arange(12).reshape(3,4)
print(a, a.shape)

f = a.flatten()
print(f, f.shape)     #1

a.flat = 255          #2
print(a)


#1 : (3,4) ----> (12,)
#2 : 임시로 1차원으로 flatten 후, 값을 255로 대입받고 다시 원래 차원으로 return 
```
`[[ 0  1  2  3]
 [ 4  5  6  7]
 [ 8  9 10 11]]`

 `(3, 4)`

`[ 0  1  2  3  4  5  6  7  8  9 10 11]`

`(12,)`

`[[255 255 255 255]
 [255 255 255 255]
 [255 255 255 255]]`

***

```python
# 데이터의 순서를 역으로 변경

a = np.arange(12).reshape(3,4)
print(a[::-1])             #1
print(a[:,::-1])           #2
print(a[::-1, ::-1])       #3

#1 : 행의 순서를 거꾸로 변경
#2 : 열의 순서를 거꾸로 변경
#3 : 행, 열의 순서를 거꾸로 변경
```
`[[ 8  9 10 11]
 [ 4  5  6  7]
 [ 0  1  2  3]]`

`[[ 3  2  1  0]
 [ 7  6  5  4]
 [11 10  9  8]]`

`[[11 10  9  8]
 [ 7  6  5  4]
 [ 3  2  1  0]]`

 ***

```python
# transpose() : 전치행렬, 행과 열을 서로 맞바꾸는 함수

t = a.transpose()      #1
print(t, t.shape)
print(a.T)             #2

#1 : a를 transpose
#2 : transpose() 함수와 동일한 결과
```
`[[ 0  4  8]
 [ 1  5  9]
 [ 2  6 10]
 [ 3  7 11]]`

 `(4, 3)`

`[[ 0  4  8]
 [ 1  5  9]
 [ 2  6 10]
 [ 3  7 11]]`

 ***
>> ### 5) numpy의 속성(Attribute) : 멤버변수, 메서드
- dtype, shape, ndim, flat, T, size, nbytes
```python
d = np.arange(12).reshape(3,4)

print(d, d.shape)
print(d.dtype)           # 데이터타입 (int 32)
print(d.ndim)            # 차원 (2차원)
print(d.T)               # transpose()
print(d.size)            # 요소의 개수 (12개)
print(d.nbytes)          # 32bit(4 byte) * 12 = 48 bytes
```
`[[ 0  1  2  3]
 [ 4  5  6  7]
 [ 8  9 10 11]]`

`(3, 4)`

`int32`

`2`

`[[ 0  4  8]
 [ 1  5  9]
 [ 2  6 10]
 [ 3  7 11]]`
 
`12`

`48`

***

>> ### 6) numpy 통계 함수들
```python
a = np.arange(12).reshape(3,4)

print(a, a.shape)                # 배열모양
print(a.max(), np.max(a))        # 최대값
print(a.min(), np.min(a))        # 최소값
print(a.sum())                   # 합계
print(a.mean())                  # 평균
print(a.std())                   # 표준편차
print(a.var())                   # 분산
print(np.median(a))              # 중앙값

print(np.percentile(a, 25))      # 1사분위 수(Q1)
print(np.percentile(a, 50))      # 2사분위 수(Q2)
print(np.percentile(a, 75))      # 3사분위 수(Q3)
```

`[[ 0  1  2  3]
 [ 4  5  6  7]
 [ 8  9 10 11]]`

`(3, 4)`

`11 11`

`0 0`

`66`

`5.5`
`3.452052529534663`

`11.916666666666666`

`5.5`

`2.75`

`5.5`

`8.25`