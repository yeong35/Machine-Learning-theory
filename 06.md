# 06: Logistic Legression

## Classification
- binary classification에서, y값이 0, 1 두 가지만 갖는다고 가정하자
- 이 때, Linear regression을 사용한다면, y값은 0과 1 두 가지만 갖는 다는 것을 알지만, y값이 0보다 작거나, 1보다 큰 경우를 만날 수 있다.
- 이것을 방지하기 위해 **Logistic regression**을 사용한다.(분류 알고리즘임을 잊지말기)
## Hypothesis representation
- Sigmoid function
    - <a href="https://www.codecogs.com/eqnedit.php?latex=h_\Theta&space;(x)=g(\Theta&space;^T&space;x)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?h_\Theta&space;(x)=g(\Theta&space;^T&space;x)" title="h_\Theta (x)=g(\Theta ^T x)" /></a>
    - <a href="https://www.codecogs.com/eqnedit.php?latex=z&space;=&space;\Theta&space;^T&space;x" target="_blank"><img src="https://latex.codecogs.com/gif.latex?z&space;=&space;\Theta&space;^T&space;x" title="z = \Theta ^T x" /></a>
    - <a href="https://www.codecogs.com/eqnedit.php?latex=g(z)&space;=&space;\frac{1}{1&plus;e^{-z}}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?g(z)&space;=&space;\frac{1}{1&plus;e^{-z}}" title="g(z) = \frac{1}{1+e^{-z}}" /></a>
    - 우리는 h<sub>&theta;</sub>(x)의 결과값을 x가 y=1일 확률을 평가할 때 사용한다.
    
    ![sigmoid_fuction](https://d3c33hcgiwev3.cloudfront.net/imageAssetProxy.v1/1WFqZHntEead-BJkoDOYOw_2413fbec8ff9fa1f19aaf78265b8a33b_Logistic_function.png?expiry=1624060800000&hmac=_Lr5yKrLltcDc7zA3doULW-7ipm2d2YoCBtIl3yTarU)
    - 결과가 0, 1만 있다고 했을 때, 확률은 아래처럼 표현한다.
    
    - <a href="https://www.codecogs.com/eqnedit.php?latex=P(y=0|x;\Theta&space;)&plus;P(y=1|x;\Theta&space;)=1" target="_blank"><img src="https://latex.codecogs.com/gif.latex?P(y=0|x;\Theta&space;)&plus;P(y=1|x;\Theta&space;)=1" title="P(y=0|x;\Theta )+P(y=1|x;\Theta )=1" /></a>

## Decision Boundary
- Decision Boundary는 y=0, 1을 결정하는 선이다.
- y>=0.5일 때, y=1이라고 가정하면
- h<sub>&theta;</sub>(x)=g(z)가 0.5보다 크거나 같을 때, y=1이라고 하는 것이다.

## Cost function for logistic regression
- 만약 cost function이 g(z)라고하면, non-covex(비볼록 함수)이기 때문에, Global minimum에 도달할 수 없다.
- 따라서 cost function을 아래와 같다고 가정하자
- <a href="https://www.codecogs.com/eqnedit.php?latex=J(\Theta&space;)=&space;\frac{1}{m}\sum_{i=1}^{m}Cost(h_\Theta&space;(x^{(i)}),&space;y^{(i)})" target="_blank"><img src="https://latex.codecogs.com/gif.latex?J(\Theta&space;)=&space;\frac{1}{m}\sum_{i=1}^{m}Cost(h_\Theta&space;(x^{(i)}),&space;y^{(i)})" title="J(\Theta )= \frac{1}{m}\sum_{i=1}^{m}Cost(h_\Theta (x^{(i)}), y^{(i)})" /></a>
- <a href="https://www.codecogs.com/eqnedit.php?latex=Cost(h_\Theta&space;(x),&space;y)=-log(h_\Theta&space;(x))" target="_blank"><img src="https://latex.codecogs.com/gif.latex?Cost(h_\Theta&space;(x),&space;y)=-log(h_\Theta&space;(x))" title="Cost(h_\Theta (x), y)=-log(h_\Theta (x))" /></a>    (if y = 1)
- <a href="https://www.codecogs.com/eqnedit.php?latex=Cost(h_\Theta&space;(x),&space;y)=-log(1-h_\Theta&space;(x))" target="_blank"><img src="https://latex.codecogs.com/gif.latex?Cost(h_\Theta&space;(x),&space;y)=-log(1-h_\Theta&space;(x))" title="Cost(h_\Theta (x), y)=-log(1-h_\Theta (x))" /></a> (if y = 0)
- y가 1일때, h(x)가 1이면 cost function의 값은 0, 0에 가까워질수록 costfuction은 무한대로 증가한다
- y가 0일때, h(x)가 0이면 cost function의 값은 0, 1에 가까워질수록 costfuction은 무한대로 증가한다
- 이것이 J(&theta;)가 logistic regression에서 볼록함수임을 보장한다.

## Simplified cost function and gradient descent 
- <a href="https://www.codecogs.com/eqnedit.php?latex=J(\Theta&space;)=\frac{1}{m}Cost(h_\Theta&space;(x^{(i)},&space;y^{i}))" target="_blank"><img src="https://latex.codecogs.com/gif.latex?J(\Theta&space;)=\frac{1}{m}Cost(h_\Theta&space;(x^{(i)},&space;y^{i}))" title="J(\Theta )=\frac{1}{m}Cost(h_\Theta (x^{(i)}, y^{i}))" /></a>
- 위의 cost function을 하나의 방정식으로 압축하면 아래와 같다.
- <a href="https://www.codecogs.com/eqnedit.php?latex=Cost(h_\Theta&space;(x),&space;y)=-ylog(h_\Theta&space;(x))-(1-y)log(1-h_\Theta&space;(x))" target="_blank"><img src="https://latex.codecogs.com/gif.latex?Cost(h_\Theta&space;(x),&space;y)=-ylog(h_\Theta&space;(x))-(1-y)log(1-h_\Theta&space;(x))" title="Cost(h_\Theta (x), y)=-ylog(h_\Theta (x))-(1-y)log(1-h_\Theta (x))" /></a>
- <a href="https://www.codecogs.com/eqnedit.php?latex=J(\Theta&space;)=-\frac{1}{m}[\sum_{i-1}^{m}-y^{i}log(h_\Theta&space;(x^{i}))-(1-y^{i})log(1-h_\Theta&space;(x^{i}))]" target="_blank"><img src="https://latex.codecogs.com/gif.latex?J(\Theta&space;)=-\frac{1}{m}[\sum_{i-1}^{m}-y^{i}log(h_\Theta&space;(x^{i}))-(1-y^{i})log(1-h_\Theta&space;(x^{i}))]" title="J(\Theta )=-\frac{1}{m}[\sum_{i-1}^{m}-y^{i}log(h_\Theta (x^{i}))-(1-y^{i})log(1-h_\Theta (x^{i}))]" /></a>
- for문을 이용하여 &theta;들을 update할 수 있지만, vectorized implementation을 사용하는 것이 더 좋다
- θ:=θ− (m/α) ​X<sup>T</sup>(g(Xθ)−y)

## Advanced optimization
- "Conjugate gradient", "BFGS", "L-BFGS"를 칭함
- Gradient descent보다 정교하고 빠르다. 그러나 직접 작성하지말고 라이브러리를 사용하길 권함.
- 장점: &alpha;값을 정하지 않아도 됨, gradient descent보다 빠를 수 있음, 내부 동작을 몰라도 사용가능
- 단점: 디버깅이 힘듦, 구현하지않는걸 권함

## Multiclass classification problems
- 병걸림, 안걸림과 같이 두 가지로 나누어지는 것이 아닌 여러개로 분류할 수 있는 것이 multiclass classification
- one-vs-all(one-vs-rest)
    - n개의 분류를 한다고 할 때, <a href="https://www.codecogs.com/eqnedit.php?latex=h_\Theta&space;^{(i)}(x)=P(y=i|x;\Theta&space;)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?h_\Theta&space;^{(i)}(x)=P(y=i|x;\Theta&space;)" title="h_\Theta ^{(i)}(x)=P(y=i|x;\Theta )" /></a>를 n개 모두 binary logistic regression 해준다.
    - 이후 새로운 x를 예측할 때, <a href="https://www.codecogs.com/eqnedit.php?latex=max(h_\Theta&space;^{(i)}(x))" target="_blank"><img src="https://latex.codecogs.com/gif.latex?max(h_\Theta&space;^{(i)}(x))" title="max(h_\Theta ^{(i)}(x))" /></a>를 (가장 큰 예측값) 선택해주면된다.