# Regularization

## The Problem of Overfitting
- Overfitting(high variance, 과적합): 모델이 학습데이터는 잘 포착하나 새로운 데이터가 들어왔을 때, 잘 포착하지 못함.
    - 복잡한 함수를 사용하거나 너무 많은 feature를 사용할 때 나타남
- Underfitting(high bias, 과소적합): 모델이 데이터를 잘 포착하지 못함. 
    - 함수가 너무 쉽거나 적은 feature를 사용할 때 나타남
- Overfitting 해결 방법
    1. feature 숫자 줄이기
        - 그냥 쓸모있어보이는 것만 쓰고 나머지 버리기
        - model selection algorithm 사용하기
    2. Regularization
        - feature들을 버리지말고, 각 &theta;의 가중치를 줄이기
        - 우리가 유용한 feature들만 있다면 꽤나 유용하게 사용됨

## Cost Function
- <a href="https://www.codecogs.com/eqnedit.php?latex=min_\Theta&space;\frac{1}{2m}\sum_{m}^{i=1}(h_\Theta&space;(x^{(i)}-y^{(i)}))^2&space;&plus;&space;1000\Theta&space;^2_3&plus;&space;1000\Theta&space;^2_4" target="_blank"><img src="https://latex.codecogs.com/gif.latex?min_\Theta&space;\frac{1}{2m}\sum_{m}^{i=1}(h_\Theta&space;(x^{(i)}-y^{(i)}))^2&space;&plus;&space;1000\Theta&space;^2_3&plus;&space;1000\Theta&space;^2_4" title="min_\Theta \frac{1}{2m}\sum_{m}^{i=1}(h_\Theta (x^{(i)}-y^{(i)}))^2 + 1000\Theta ^2_3+ 1000\Theta ^2_4" /></a>
- 이런 cost function이 있다고 할 때, &theta;3과 4를 0에 근사하게 만들어 줌으로써 cost function의 값을 줄일 수 있다.
- 요약하면 아래처럼 함으로써 정규화할 수 있다.
- <a href="https://www.codecogs.com/eqnedit.php?latex=min_\Theta&space;\frac{1}{2m}\sum_{m}^{i=1}(h_\Theta&space;(x^{(i)}-y^{(i)}))^2&space;&plus;&space;\lambda&space;\sum_{j=1}^{n}\Theta&space;^2_j" target="_blank"><img src="https://latex.codecogs.com/gif.latex?min_\Theta&space;\frac{1}{2m}\sum_{m}^{i=1}(h_\Theta&space;(x^{(i)}-y^{(i)}))^2&space;&plus;&space;\lambda&space;\sum_{j=1}^{n}\Theta&space;^2_j" title="min_\Theta \frac{1}{2m}\sum_{m}^{i=1}(h_\Theta (x^{(i)}-y^{(i)}))^2 + \lambda \sum_{j=1}^{n}\Theta ^2_j" /></a>
- 이때 람다는 regularization parameter라고 한다. 람다가 theta값들이 얼마나 키울 것인지 결정한다
- 우리는 과적합을 줄임으로써 우리의 가설함수를 smooth하게 만들 수 있다.
- 람다가 만약 너무 크다면? -> underfitting

## Regularized Linear Regression
- 정규화가 없었던 gradient descent
    - ![정규화 안하는 gradient descent](http://www.holehouse.org/mlclass/07_Regularization_files/Image%20[5].png)
- 정규화가 있는 gradient descent
    - ![정규화하는 gradient descent](http://www.holehouse.org/mlclass/07_Regularization_files/Image%20[6].png)
    - ![위를 살짝 바꾼 식](http://www.holehouse.org/mlclass/07_Regularization_files/Image%20[7].png)
- ![1-alpha*ramda/m](http://www.holehouse.org/mlclass/07_Regularization_files/Image%20[9].png)
    - 위 수는 대게 1보다 작다.
    - 위 수는 대게 learning rate보다는 작고 m보다는 크다
    - &theta;<sub>0</sub>은 제외!

## Regularized Logistic Regression
- ![regularizedLogisticRegression](https://d3c33hcgiwev3.cloudfront.net/imageAssetProxy.v1/dfHLC70SEea4MxKdJPaTxA_306de28804a7467f7d84da0fe3ee9c7b_Screen-Shot-2016-12-07-at-10.49.02-PM.png?expiry=1624406400000&hmac=m9Gl4zWKJID-15CqIcIaQD08E5pXZ_hnzovb_dr0qLU)
- 0은 아래 식으로 업데이트하지않고 위의 식으로 업데이트한다.