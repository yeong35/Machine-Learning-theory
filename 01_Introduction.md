# 01 and 02: Introduction, Regression Analysis, and Gradient Descent

## Machine Learning이란?
- Arthur Samuel(1959)
    - "명시적으로 프로그래밍 없이 컴퓨터가 학습하는 능력을 만들어주도록 공부하는 분야"
- Tom Michel(1999)
    - "컴퓨터 프로그램이 어떤 종류의 과제 T, 측정된 결과 P로 인해 경험 E가 학습된다고 말해진다.T가 수행되고, P로 측정하면 할수록, E가 더 개선되는 것이다."

## Machine Learning의 종류
- Supervised leaning(지도 학습)
- Unsupervised leaning(비지도학습)
- Redinforcement leaning(강화 학습)
- Recommender systems(추천 시스템)

## Supervised learning - 소개
- machine learning의 가장 흔한 문제 타입
- 미지의 data가 들어왔을 때, **training data**(data와 result set)를 활용하여 더욱 옳은 답을 만들어 내는 알고리즘
    1. **regression problem** 
        - 연속적인 값의 output
        - 이산적인 값으로 표현할 수 없음
        - ex) 몇몇 집의 크기와 가격이 주어졌을 때, 집의 크기로 집값의 가격을 예상해보자.
    2. **classification problem**
        - 이산 적인 값(또는 n개)으로 표현할 수 있음
        - ex) 종양의 크기가 주어졌을 때, 유방암에 걸렸는지 아닌지를 예상해보자.

## Unsupervised leaning - 소개
- 두 번째로 주된 문제 타입
- **unlabled data**를 이용
    1. **Clustering algorithm**
        - n개의 그룹으로 구분짓는 것
        - ex) n개의 뉴스기사를 가장 유사하다고 생각되는 것끼리 그룹짓는 것
    2. **Cocktail party algorithm**
        - cocktail party problem
            - 화자로부터 마이크가 각각 다른 위치로 놓여져있다. 이때 누가 말한 것인지 분리해보자.

## Linear Regression
- 표기법
    - m = training example 개수
    - x's = input 또는 특징
    - y's = output
        - (x, y) - single training 예시
        - (x<sup>i</sup>, y<sup>i</sup>) - 특정 예시, i는 index
    - hypothesis _h_
        - h<sub>&theta;</sub>(x) = &theta;<sub>0</sub> + &theta;<sub>1</sub>x
            - &theta;<sub>i</sub>는 parameters
                - &theta;<sub>0</sub>는 상수, &theta;<sub>1</sub>는 기울기
            - 위 함수를 **linear regression** 또는 **univariate linear regression**라 함

## Linear regression - implementation(cost function)
- Hypothesis - x가 주어질 때, prediction machine가 예상하는 y의 값
- cost - training data를 사용하여 &theta;를 결정한다. 이것을 이용하여 *h*를 더 정확하게 만들 수 있다.

### cost function(squared error cost function)
- <a href="https://www.codecogs.com/eqnedit.php?latex=J(\theta_0,&space;\theta_1)=\frac{1}{2m}\sum_{i=1}^{m}(h_\theta(x^i)-y^i)^2" target="_blank"><img src="https://latex.codecogs.com/gif.latex?J(\theta_0,&space;\theta_1)=\frac{1}{2m}\sum_{i=1}^{m}(h_\theta(x^i)-y^i)^2" title="J(\theta_0, \theta_1)=\frac{1}{2m}\sum_{i=1}^{m}(h_\theta(x^i)-y^i)^2" /></a>
    - 1/m - 평균을 구하기위해 합을 m으로 나눈 것
    - 왜 2로 또 나누는 가? - 수학계산을 좀 더 쉽게하기 위함. 그리고 2로 나눈다고 해서 상수는 바뀌지 않음
- 사용이유
    1. parameter들을 결정함
    2. parameter와 관련된 값들은 *h*가 어떻게 행동할지를 결정함.
- J(&theta;<sub>0</sub>, &theta;<sub>1</sub>)가 가장 작은 값이 되었을 때, learning algorithm에 최적화되었다고 한다.

## Gradient descent algorithm
- J를 최소화하기위해 사용됨
- 모든 machine learning에서 최소화를 하기위해 사용되는 알고리즘
- J(&theta;<sub>0</sub>, &theta;<sub>1</sub>)을 알고있을 때, min J(&theta;<sub>0</sub>, &theta;<sub>1</sub>)을 찾아보자

- 어떻게 동작하는 가?
    1. (0, 0)에서 시작, 또는 아무 좌표
    2. J(&theta;<sub>0</sub>, &theta;<sub>1</sub>)가 줄어들 때까지 &theta;<sub>0</sub>, &theta;<sub>1</sub>를 바꿈
    3. 2를 반복
    4. local minimum에 도달하면 멈춤

- <a href="https://www.codecogs.com/eqnedit.php?latex=\Theta&space;_j&space;:=\Theta&space;_j&space;-&space;\alpha&space;\frac{d&space;}{d&space;\Theta&space;_j}J(\Theta&space;_0,&space;\Theta_1)&space;(for&space;j=0&space;and&space;j=1)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\Theta&space;_j&space;:=\Theta&space;_j&space;-&space;\alpha&space;\frac{d&space;}{d&space;\Theta&space;_j}J(\Theta&space;_0,&space;\Theta_1)&space;(for&space;j=0&space;and&space;j=1)" title="\Theta _j :=\Theta _j - \alpha \frac{d }{d \Theta _j}J(\Theta _0, \Theta_1) (for j=0 and j=1)" /></a>
    - :=는 업데이트, =는 할당
    - &alpha;는 learning rate로 커지면 gradient desecent가 빠르게 변하고, 작으면 조금씩 변한다
    - 이 작업을 &theta;<sub>0</sub>, &theta;<sub>1</sub> **동시**에 해준다.