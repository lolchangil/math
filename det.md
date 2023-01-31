## 행렬식 구하는 알고리즘
일단 재귀함수로 만들어봐야겠다

일단 알고리즘의 도식도를 짜보자

----

- A = 모행렬 (이렇게 적어도 되나?)
- l = 정사각행렬의 크기
- i = 행
- j = 열

```
function submatrix(A, i, j, l){ // 소행렬을 구하는 함수
    A에서 i행과 j열 삭제
}

function det(A, l){ // 행렬식을 구하는 함수
    if(l==2)
        return A[11]*A[22] - A[12]*A[21]
    else{
        value = 0
        row = 1 //변할 수 있음, 허나 row <= l 이어야함
        for 0 ... l as i { // i는 열을 나타냄
            num = a[row i] * det(submatrix(A,row,i,l), l-1)
            if(i%2) //짝수 열 일시
                num *= -1
            value += num 
        }
        return value
    }
}
```

----

이걸 실제 코드로 구현해보자

----

```python
from sage.all import *
A = matrix(QQ,[[0,1,2],[3,4,5],[6,7,8]])
B = matrix(QQ,[[0,1,2],[3,4,5],[6,7,9]])
print(A.det())
print(B.det())
# 0
# -3
```
참 좋은 프로그램인 sagemath를 사용하면 이렇게 쉽고 빠르게 사용가능하지만, 이러면 공부하는 의미가 없기에 위의 짜논 도식도대로 코드를 짜보았다.

```python
# 행렬식
# 일단 일차원 배열로 받기로 했다.

import math

def submatrix(A, i, j, l): # 소행렬를 구하는 식
    new = []
    for x in range(l):
        for y in range(l):
            if x == i or y == j:
                pass
            else:
                new.append(A[x*l+y])
    return new

def det(A, l): # 행렬식을 구하는 함수
    if l==2:
        return A[0]*A[3] - A[1]*A[2]
    else:
        value = 0
        row = 1 # 변할 수 있음, 허나 row <= l 이어야함
        row -= 1
        for i in range(l):
            num = A[row*l+i] * det(submatrix(A,row,i,l), l-1)
            if(i%2==1):
                num *= -1
            value += num
        return value

def determinant(A): # 실제 호출 함수
    if len(A) == 0:
        return 0
    elif len(A) == 1:
        return A[0]
    else:
        l = math.sqrt(len(A))          
        if l.is_integer():
            return det(A,int(l))
        else:
            print("정사각행렬이 아닙니다.")
            return

A = [0,1,2,3,4,5,6,7,9]
print(determinant(A))
# -3
```

----

자신이 이해를 하지 못한다면 그것은 1/2확률로 당신이 선형대수학을 모르는 것이다

*뭔가 코드에 문제가 있다면 알려주세요!*