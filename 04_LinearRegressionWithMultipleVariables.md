# 04: Linear Regression with Multiple Variables

## Linear regression with muliple features
- Multiple variables = multiple features
- 만약, 새 sheme에서 다양한 변수들이 주어진다면...(4개의 변수를 갖는다고 가정하자.)
    - x<sub>1</sub> - size(feet squared)
    - x<sub>2</sub> - Number of bedrooms
    - x<sub>3</sub> - Number of floors
    - x<sub>4</sub> - Age of home(years)
    - y - output variale(price)
- More notation
    - n - number of features
    - m - number of examples
    - x<sup>i</sup> - vector of the input for an example
    - x<sub>j</sub><sup>i</sup> - The value of feature j in the *i*th training example
- h<sub>&theta;</sub>(x)=&theta;<sub>0</sub>+&theta;<sub>1</sub>x<sub>1</sub>+&theta;<sub>2</sub>x<sub>2</sub>+&theta;<sub>3</sub>x<sub>3</sub>+&theta;<sub>4</sub>x<sub>4</sub>
- h<sub>&theta;</sub>(x)=&theta;<sup>T</sup>X 로 표현이 가능하다.
    - &theta;는 열벡터, &theta;<sup>T</sup>는 행벡터


## Gradient descent for multiple variables
- Parameter가 0부터 n까지 있을 때, vector(&theta;)라고 생각하자. &theta;는 [n+1 x 1] 벡터
- cost function은...
    - <a href="https://www.codecogs.com/eqnedit.php?latex=J(\Theta_0&space;,\Theta&space;_1&space;,&space;...,&space;\Theta&space;_n&space;)&space;=\frac{1}{2m}\sum_{i=1}^{m}(h_\Theta&space;(x^{(i)})-y^{(i)}&space;)^2" target="_blank"><img src="https://latex.codecogs.com/gif.latex?J(\Theta_0&space;,\Theta&space;_1&space;,&space;...,&space;\Theta&space;_n&space;)&space;=\frac{1}{2m}\sum_{i=1}^{m}(h_\Theta&space;(x^{(i)})-y^{(i)}&space;)^2" title="J(\Theta_0 ,\Theta _1 , ..., \Theta _n ) =\frac{1}{2m}\sum_{i=1}^{m}(h_\Theta (x^{(i)})-y^{(i)} )^2" /></a>
- Gradient descent는
    - <a href="https://www.codecogs.com/eqnedit.php?latex=\Theta&space;_j&space;:=&space;\Theta&space;_j&space;-&space;\alpha&space;\frac{1}{m}\sum_{i=1}^{m}(h_\Theta&space;(x^{(i)})-y^{(i)}&space;)x^{(i)}_{j}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\Theta&space;_j&space;:=&space;\Theta&space;_j&space;-&space;\alpha&space;\frac{1}{m}\sum_{i=1}^{m}(h_\Theta&space;(x^{(i)})-y^{(i)}&space;)x^{(i)}_{j}" title="\Theta _j := \Theta _j - \alpha \frac{1}{m}\sum_{i=1}^{m}(h_\Theta (x^{(i)})-y^{(i)} )x^{(i)}_{j}" /></a>
    - 위를 (0부터 n까지 동시에) 반복하는 것이다!
- 다른 말로는...
    - <a href="https://www.codecogs.com/eqnedit.php?latex=\Theta&space;_j&space;:=&space;\Theta&space;_j&space;-&space;\alpha&space;\frac{d}{d\theta_j&space;}J(\theta)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\Theta&space;_j&space;:=&space;\Theta&space;_j&space;-&space;\alpha&space;\frac{d}{d\theta_j&space;}J(\theta)" title="\Theta _j := \Theta _j - \alpha \frac{d}{d\theta_j }J(\theta)" /></a>
- 아래의 식을 잘 기억해두자
    - <a href="https://www.codecogs.com/eqnedit.php?latex=\frac{1}{m}\sum_{i=1}^{m}(h_\Theta&space;(x^{(i)})-y^{(i)}&space;)x^{(i)}_{j}&space;=&space;\frac{d}{d\Theta&space;_j&space;}J(\Theta&space;)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\frac{1}{m}\sum_{i=1}^{m}(h_\Theta&space;(x^{(i)})-y^{(i)}&space;)x^{(i)}_{j}&space;=&space;\frac{d}{d\Theta&space;_j&space;}J(\Theta&space;)" title="\frac{1}{m}\sum_{i=1}^{m}(h_\Theta (x^{(i)})-y^{(i)} )x^{(i)}_{j} = \frac{d}{d\Theta _j }J(\Theta )" /></a>
## Gradient Decent in practice: 1 Feature Scaling
- feature들을 비슷한 scale로 만들어주면? -> gradient descent가 더 빨리 minimum에 도달할 수 있다
    - ex) 1~50000, 1~100이면 찾기가 더 힘들 것임
- iteration을 몇으로 할 지는 선택하기 어려워
    - x축을 iteration 수, y를 min J(&theta;)라고 할 때, 그래프가 직선이 되는 곳을 찾으면 편함
- x축을 iterations, y축을 J(&theta;)로 둘 때, minimum이 증가한다면, &alpha;(learning rate)가 너무 큰 것
- 만약 이상한 input이 들어와 gradient descent를 한다면?
    - input을 더욱 효율적으로 rescale 해야함
    - 각 특징을 x1, x2로 정의한다며, 이들을 각각의 최대값으로 나누어주어야함 (**mean normalization**)
    - <a href="https://www.codecogs.com/eqnedit.php?latex=x_1&space;\leftarrow&space;\frac{x_1&space;-&space;\mu&space;_1}{s_1}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?x_1&space;\leftarrow&space;\frac{x_1&space;-&space;\mu&space;_1}{s_1}" title="x_1 \leftarrow \frac{x_1 - \mu _1}{s_1}" /></a>
        - &mu;=x<sub>1</sub>의 평균값
        - s<sub>1</sub>=(max-min) 또는 표준편차

## Learning Rate &alpha;  
- learning rate &alpha;에 대해 알아보자
    - update rule
    - debugging
    - 어떻게 alpha를 정하는 가?
- gradient descent가 제대로 작동한다면, J(&theta;)는 실행할때마다 감소할 것이다
- learning rate가 너무 크다면? -> J(&theta;)가 감소하지 않을 수 있다
- learning rate가 너무 작다면? -> 각 실행마다 조금씩 감소함
- 다양한 alpha값을 사용하는 것이 좋음
- alpha값을 **3배씩 증가시켜보자**
    - ex) 0.001, 0.003, 0.01, ..., 0.3
    
## Features and polynomial regression
- 특징을 선택하는 것과, 적절한 특징을 선택함으로써 어떻게 다양한  learning algorithms을 얻을 수 있을까?
- polynomial(다항식) regression은 non-linear function

## Normal equation
- 몇 linear regression 문제에서, normal equation이 좋은 해답을 얻게 도와줄 수 있을 것이다!
- normal equation은 &theta;를 분석적으로 해결할 수 있다.
- 동작방법
    - X라는 design matrix를 구성하고, 이것이 모든 특징을 갖게하자(n * n+1)
    - &theta;=(X<sup>T</sup>X)<sup>-1</sup>X<sup>T</sub>y
        - 위를 계산하면 &theta;를 알 수 있음

    - Gradient descent
        - learning rate를 선택해야 할 때
        - 많은 iteration이 필요할 때(이건 theta값 찾기가 조금 느려짐)
        - n이 너무 클 때
            - 100~1000은 작은 편임, 10000부터 크다 할 수 있음
    - Normal equation
        - learning rate를 선택하지 않아도 됨
        - iterate가 필요 x
        - (X<sup>T</sup>X)<sup>-1</sup>를 계산해야함
## Normal equation and non-invertibility
- (X<sup>T</sup>X)<sup>-1</sup>가 비가역적이라면?
    1. 필요없는 특징이 있다
    2. 특징이 너무 많다
- 해결 방법은?
    - 특징을 지운다
        - 특징이 linearly dependent? -> 지우세요
    - regularization을 사용한다.