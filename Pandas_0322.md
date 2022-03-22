2022.03.22
# 모듈(Module)
- 모듈 : 변수, 함수, 클래스를 모아놓은 `.py` 확장자 파일
- `.py` 파일 : 파이썬 코드만
- 패키지 : 모듈의 기능을 디렉토리(폴더) 별로 정리해 놓은 개념

1. `%%writefile [filepath]` : `[filepath]` 경로에 `.py` 파일을 작성
2. `import 모듈명` : 모듈을 불러오는 키워드
3. `from 모듈명 import [변수명 또는 함수명 또는 클래스명]` : 모듈 내에 있는 함수, 변수, 클래스를 따로 따로 불러오기  
4. `import 모듈명 as 별명` : 모듈을 불러올 때 별명 지어주기(alias)
5. `from demo import *` : 모듈 내의 모든 항목 불러오기

# 패키지(Package) 
1. `!mkdir [directory path]` : directory path 경로에 디렉토리를 생성  
활용1 : `!mkdir -p mc_pkg/pkg1`  
활용2 : `!apt-get install tree` -> 이쁘게 도식



# Pandas
- 파이썬에서 데이터를 시각적으로 간편하게 다룰 수 있도록 만들어진 라이브러리
- 2차원 배열 데이터에 대한 집계, 시각화, 편집 굉장히 쉽게 해준다.

## numpy를 활용해서 데이터의 모양(shape)알아보기
numpy란?
- 수치 계산을 하기 위한 파이썬 모듈
- 배열에 대한 병렬 연산에 특화

## 1. `numpy`의 배열을 `ndarray`
``` python
# numpy 모듈 import
import numpy as np
# 파이썬의 list를 ndarray화 하기
py_list = [1, 2, 3]
arr = np.array(py_list)
arr
-> array([1, 2, 3])
```

## 2. 배열의 종류
1. 스칼라(scalar)
  * 0차원 데이터
  * 단순하게 측정한 하나의 값
2. 벡터(vector)
  * 1차원 데이터( 1차원 배열 )
  * **스칼라가 연속적으로 여러 개 모여 있는 것**
  * 백터 내에 데이터가 `N`개가 있으면 `N 차원 벡터`라고 한다.
    * 수학적인 표현에서의 표현 : 행 벡터, 열 벡터 가리지 않고 `N 차원 벡터`로 표현
    * 데이터 사이언스에서의 표현 - 일반적으로는 **행 벡터에 대해서만** `N차원 벡터`로 표현한다.
3. 행렬(Matrix)
  * 2차원 데이터( 2차원 배열 )
  * 1차원 배열인 벡터가 여러 개 모여 있는 것
4. 텐서(Tensor)
  * 3차원 이상의 데이터 ( 3차원 이상의 배열 )
  * `N 차원 배열`을 그냥 텐서라고 한다.
    * `0 Rank Tensor` - 스칼라
    * `1 Rank Tensor` - 벡터
    * **`2 Rank Tensor` - 행렬**
    * `3 Rank Tensor` - 텐서
**2 Rank Tensor(행렬) 부터 머신러닝 라이브러리 및 딥러닝 프레임워크에 넣을 수 있음**

## 3. `numpy` 함수 알아보기
1. np.arange
```python
np.arange(1,10,2)
-> array([1, 3, 5, 7, 9])
```
2. 다차원 배열만들기
- 2차원 이상의 배열(형렬 이상)을 다차원 배열
 * `np.arange()` : 1차원 정수 배열 만들기
  * `np.zeros()` : 0으로 채워진 0 행렬(`zero-vector`)를 만들 때 사용
  * `np.ones()` : 1로 채워진 1 행렬(`ones-vector`)를 만들 때 사용
  * `np.full()` : 지정한 숫자로 채워진 행렬를 만들 때 사용
  ```python
  np.zeros((2,3))
  -> array([[0., 0., 0.],
       [0., 0., 0.]])
  ```  
  ```python
  np.zeros((3, 2, 3, 4))
  -> array([[[[0., 0., 0., 0.],
         [0., 0., 0., 0.],
         [0., 0., 0., 0.]],

        [[0., 0., 0., 0.],
         [0., 0., 0., 0.],
         [0., 0., 0., 0.]]],


       [[[0., 0., 0., 0.],
         [0., 0., 0., 0.],
         [0., 0., 0., 0.]],

        [[0., 0., 0., 0.],
         [0., 0., 0., 0.],
         [0., 0., 0., 0.]]],


       [[[0., 0., 0., 0.],
         [0., 0., 0., 0.],
         [0., 0., 0., 0.]],

        [[0., 0., 0., 0.],
         [0., 0., 0., 0.],
         [0., 0., 0., 0.]]]])
   # 4차원 배열
   # 3차원 배열의 개수 : 3개씩
   # 2차원 배열의 개수 : 2개씩
   # 1차원 배열의 개수 : 3개씩
   # 0차원 데이터 개수 : 4개씩       
   ```
3. 단위 행령(항등 행렬)만들기
- `np.eye`, `np.identity`
```python
np.eye(3,4)
-> array([[1., 0., 0., 0.],
       [0., 1., 0., 0.],
       [0., 0., 1., 0.]])
```
4. 대각 행렬
- 주 대각 방향만 값이 차있고 나머지 방향은 0인 행렬
``` python
np.diag(np.arrange(1,10,2))
array([[1, 0, 0, 0, 0],
       [0, 3, 0, 0, 0],
       [0, 0, 5, 0, 0],
       [0, 0, 0, 7, 0],
       [0, 0, 0, 0, 9]])
```
5. 점 구간 만들기(사잇값 만들기)
- 시각화 예시로 자주 사용.
```python
# 1~10까지 3개의 숫자를 이용해 2개의 구간에 균등하게 만들어준다.
np.linspace(1,10,3)
-> array([ 1. ,  5.5, 10. ])
```
4. axis 이해하기
`axis` : 축. 데이터가 추가되는 방향, 그 방향에 대한 **인덱스**

예를 들어 3차원 배열 `(3, 4, 5)`
* 3차원 배열에 추가되는건 2차원 배열 -> `axis : 0`
* 2차원 배열에 추가되는건 1차원 배열 -> `axis : 1`
* 1차원 배열에 추가되는건 0차원 스칼라 -> `axis : 2`

예를 들어 (3,4,5) 일때   
3차원 배열 -> 2차원 배열 axis : 0, => 2차원 배열끼리 비교하겠다.  
2차원 배열 -> 1차원 배열 axis : 1, => 1차원 배열끼리 비교하겠다.  
1차원 배열 -> 0차원 배열 axis : 2, => 0차원 스칼라 비교하겠다.
```python
np.random.seed(42)
arr= np.random.randint(1,37,(3,2,3))
arr
-> array([[[29, 15,  8],
        [21, 19, 23]],

       [[11, 11, 24],
        [36, 24,  3]],

       [[22,  2, 24],
        [30,  2, 21]]])

# 축별 최대값
np.max(arr, axis=0)
# 3차원 배열안 2차월 배열에서 각각 비교
-> array([[29, 15, 24],
       [36, 24, 23]])

np.max(arr,axis=1)
# 2차원 배열안 1차열 배열에서 각각 비교
-> array([[29, 19, 23],
       [36, 24, 24],
       [30,  2, 24]])

np.max(arr,axis=2)
# 1차원 배열안 스칼리 비교
-> array([[29, 23],
       [24, 36],
       [24, 30]])
```

```python
np.random.seed(42)
arr = np.random.randint(1, 37, (2, 2, 3, 2))
arr
-> array([[[[29, 15],
         [ 8, 21],
         [19, 23]],

        [[11, 11],
         [24, 36],
         [24,  3]]],


       [[[22,  2],
         [24, 30],
         [ 2, 21]],

        [[33, 12],
         [22, 25],
         [27, 28]]]])
# (2, 2, 3, 2)
np.max(arr, axis=1)
-> array([[[29, 15],
        [24, 36],
        [24, 23]],

       [[33, 12],
        [24, 30],
        [27, 28]]])

## 4. 인덱스
```python
np.random.seed(42)
arr = np.random.randint(1,11,(2,5))
arr
-> array([[ 7,  4,  8,  5,  7],
       [10,  3,  7,  8,  5]])
arr[0]
-> array([7, 4, 8, 5, 7])
arr[0][2] # arr[0,2]와 동일 표현
-> 8
```

## 5. 슬라이싱
```python
np.random.seed(42)
arr = np.random.randint(1, 37, (2, 2, 3, 2))
arr
-> array([[[[29, 15],
         [ 8, 21],
         [19, 23]],

        [[11, 11],
         [24, 36],
         [24,  3]]],


       [[[22,  2],
         [24, 30],
         [ 2, 21]],

        [[33, 12],
         [22, 25],
         [27, 28]]]])

arr[:, :, ::2, :]
-> array([[[[29, 15],
         [19, 23]],

        [[11, 11],
         [24,  3]]],


       [[[22,  2],
         [ 2, 21]],

        [[33, 12],
         [27, 28]]]])
```





