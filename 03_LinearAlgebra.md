# 03: Linear Algebra 복습

## Matrices - overview
- 2D행렬로 표현
- 이름은 대문자로 표기(A, B, X, Y)
- Dimension 표현은 [row x col]
- R<sup>[r x c]</sup>은 r이 row, c가 col
- A<sub>(i, j)</sub>는 i<sup>th</sup> row, jth column

## Vectors - overview
- n by 1 matrix는 소문자로 표기(a, b, x, y)
- n by 1은 n dimentional vector라 칭함
- 또는 Rn(ex, R4)
- v<sub>i</sub> = i<sup>th</sup>번째 vector element

## Matrix manipulation
- Addition
    - 같은 dimention끼리만 더할 수 있음
- Multiplication by scalar
    - Scalar = real number
    - 각 요소를 Scalar 값과 곱해주면 됨
- Division by a scalar
    - 각 요소들 Scalar 값으로 나누면 됨
- Combination of operands
    - 곱셈부터 진행
- Matrix by vector multiplication
    - 각 행과 벡터 열을 곱한 후 더함
    - [a x b] * [b x c] = [a x c]
    - 이 때, 행렬 x 벡터라면, c = 1
    - 결과는 [a x 1] 벡터
- Matrix-matrix multiplication
    - A x B = C
        - A = [m x n]
        - B = [n x o]
        - C = [m x o]
    - B에서 한 열을 벡터로 생각하고, A의 각 열을 B의 한 열과 곱한 후 더한다.(행렬x벡터 곱 연산)
    - 이를 반복

## Marix multiplication properties
- <b>교환 법칙은 성립하지 않는다.</b>
- 결합 법칙은 성립한다.

- Identity matrix란?
    - matrix[i][j], i==j면 1, 아니면 0인 행렬
- 만약, A x B 행렬을 곱할 때, B가 Identity matrix라면 교환 법칙이 성립한다.
## Inverse and transpose operations
1. Matrix Inverse
    - 역수란?
        - a x b = 1일 때, a는 b의 역수, b는 a의 역수이다.
    - 모든 수는 역수를 갖고있으나, 실수의 영역에서는 <b>모든 수가 역수를 갖지는 않는다.</b> 
    - ex, 0은 역수가 없음
    - matrix에선?? 
        - 만약, A가 [m x m]라면, A의 역수는 A<sup>-1</sup>
        - 둘을 곱한다면, A*A<sup>-1</sup>=I
        - 오직 [m x m]행렬만 역수를 가질 수 있다.
        - 만약, A의 모든 element가 0이면 inverse matrix를 가질 수 없다.
2. Matrix transpose
- n x m을 m x n 행렬로 바꾸기 위해선...
- row와 column을 바꾸면 된다!