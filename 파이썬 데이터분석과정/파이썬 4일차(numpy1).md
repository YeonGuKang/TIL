# 4일차 - 아주아주 강력한 numpy

넘파이의 가장 큰 장점은 연산이 빠르고, 연산을 쉽게해주고\
모든 연산이 함수로써 존재한다는 것이다.

Numpy array (배열, 행렬)\
numpy 연산의 기본이 되는 데이터 구조입니다.\
리스트보다 간편하게 만들 수 있으며 연산이 빠른 장점이 있습니다.\
브로드캐스팅 연산을 지원합니다.\
단, 같은 type의 데이터만 저장 가능합니다.

array 또한 numpy의 기본 함수로서 생성 가능합니다.\
array 함수 호출 기본구조

ex) np.array(배열변환 대상 데이터)\
ex) np.arange(start, end, step_forward)

예를 들면 list의 합은 서로의 list를 추가해서 나열해주는 것이다\
하지만 numpy변환을 거친 array는 서로의 value의 합이다.

ex))

list1=[1,2]\
list2=[3,4]\
list3 = list1 + list2 -> [1,2,3,4]

arr1=[1,2]\
arr2=[3,4]\
arr3 = arr1 + arr2 -> [4,6]

### array 덧셈, 뺄셈, 곱셈, 나눗셈
test_array / 5

이런식의 연산도 가능하다

이처럼 강력한 함수들이 많이 존재하며 연산이 어마어마하게 빠르다.\
정말 빠르고 강력한 함수들은 python_numpy 쥬피터노트북에서 확인

###넘파이를 import 하고 np라는 닉네임으로 사용한다.
import numpy as np
### 관례적으로 np라는 약자를 많이 사용하게 됩니다.
### 파이썬을 사용하는 대부분의 유저들이 사용하고 있는 닉네임이니 이건 꼭 지켜서 사용해주시는 것을 추천드립니다.

### 기존 데이터 구조를 array로 변환
test_array = np.array(test_list)\
test_array2 = np.array(test_list2)\
test_farray = np.array(test_flist)\
test_array_2nd = np.array(test_list_2nd)\
test_array_3rd = np.array(test_list_3rd)

ex) np.arange(start, end, step_forward)

### np.arange 함수로 생성
range_array = np.arange(10)\
range_array

결과는 : array([0, 1, 2, 3, 4, 5, 6, 7, 8, 9]) 편리하게 linear한 값 가능

# 범위설정
# range() 함수와 비슷하게 작동함
np.arange(0, 100, 2)

# reshape을 통하여 행렬의 형변환이 가능
index_test = np.array(range(10))\
index_test2 = np.array(range(25)).reshape([5, 5])\
index_test3 = np.array(range(27)).reshape([3, 3, 3])

