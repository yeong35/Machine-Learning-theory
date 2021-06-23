# 09 Neural Networks - Learning
## Cost Function
- L: 총 layer 수
- S<sub>l</sub> : l layer의 unit 개수
- K : output unit 수
- 다중분류를 한다면 아래와 같은 식(cost function)을 결과마다 계산해야한다
    - ![backpropagation이없는식](http://www.holehouse.org/mlclass/09_Neural_Networks_Learning_files/Image%20[3].png)

## Backpropagation
- 우리가 gradient descent하는 것처럼 cost function을 줄여줌
- 내가 만들어낸 error를 이용해서, 각 layer(input layer전까지!)마다 거꾸로 계산해나가는 것이다
- 각 unit마다 계산된 **error**는 **partial derivatives**(편미분)를 계산함으로써 사용될수있다.
- &Theta;를 update하고, cost function을 줄이기 위해 사용
- 다음으로 넘어가기 전에 기억할 것
    - &Theta;는 각 layer의 matrix다
    - 마찬가지로 &Delta;가 각 layer마다 있는 matrix다.
- &Theta;<sub>ij</sub><sup>l</sup>i
    - i : l+1layer의 unit
    - j : layer unit
    - l : 내가 mapping해야하는 layer
    - NB(number) : destination node, origin node, origin layer로, 교수님이 만든 단어임
### Backpropagation이 무엇인가?
- partial derivatives를 사용하는 것!
- 각 node에 &delta;<sub>j</sub><sup>l</sup> : l layer에 j node의 error
    - &delta;<sub>j</sub><sup>l</sup> = a<sub>j</sub><sup>l</sup>-y<sub>j</sub>
    - a<sub>j</sub><sup>l</sup> == h<sub>&theta;</sub>(x)<sub>j</sub>
- <a href="https://www.codecogs.com/eqnedit.php?latex=\frac{d}{d\Theta_{ij}^{(l)}&space;}J(\Theta&space;)=a_j^l\delta&space;_i^{l&plus;1}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\frac{d}{d\Theta_{ij}^{(l)}&space;}J(\Theta&space;)=a_j^l\delta&space;_i^{l&plus;1}" title="\frac{d}{d\Theta_{ij}^{(l)} }J(\Theta )=a_j^l\delta _i^{l+1}" /></a>
- backpropagation을 하면서 delta를 계산함으로써, partial derivative(편미분) terms을 계산할 수 있다.

## Backpropagation Intuition
- formal하게 &delta;는 ![delta](http://www.holehouse.org/mlclass/09_Neural_Networks_Learning_files/Image%20[25].png)
- &delta;를 [a-y]라 하자
- 아래와같이 계산하면 된다.
- ![howToCalculateDelta](http://www.holehouse.org/mlclass/09_Neural_Networks_Learning_files/Image%20[27].png)  
    - &delta;와 &delta; 값은 다음 layer의 &delta;값과 weight곱의 합이다.

## Gradient checking
- Backpropagaton을 하면서 많은 버그가 생길 수 있음(J(&Theta;)가 감소하는 척 하면서 내 생각보단 안 감소되는 등..)
- 이것을 방지하기 위해 기울기를 계속 확인함!
- Vector일 경우, 아래와같이 사용될 수 있음
- ![vector&Theta;](http://www.holehouse.org/mlclass/09_Neural_Networks_Learning_files/Image%20[32].png)

## Random Initialzation
- 모든 &Theta; value들이 random하게 작은 초기값을 선택해야함
    - 다 0이게 된다면, 각 layer들이 다 같은 값(0)을 갖게될거임
- 그래서 0~1 사이에서 랜덤하게 선택해줘야한다!

## Putting it Together
1. network architecture 고르기
    - Input units : x(feature vector) 차원의 개수 고르기
    - Output units : 분류 문제의 분류 개수 고르기
    - Hidden units : default는 한 개, 각 layer마다 동일한 개수의 unit을 갖거나, input보다 1.5~2배 많은 unit을 가짐
        - Hidden unit이 많을 수록 좋아, 하지만 많을수록 계산량이 커짐
2. neural network 학습시키기
    1. 0에 근사하는 &Theta;값 설정하기
    2. x<sup>i</sup>마다 h<sub>&Theta;</sub>(x)<sup>i</sup>구하면서 forward propagation하기
    3. cost function J(&Theta;)계산하기
    4. backpropagation하면서 partial derivatives 계산하기
    5. J(&Theta;)의 추정값과 계산된 partial derivatives랑 비교하면서 기울기 확인하기
    6. gradient descent나 advanced optimization을 backpropagation에 이용하면서 J(&Theta;)값 줄이기