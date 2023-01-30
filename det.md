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
내일은 이걸 실제 코드로 구현해보자