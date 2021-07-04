# Large Scale Machine Learning
## Learning with large datasets
- 왜 large dataset을 사용해야될까?
    - 높은 성능을 내는 좋은 방법 중 하나는 low bias 알고리즘과 많은 data set을 사용하는 것입니다
        - ex) 헷갈리는 단어 classification
        - 알고리즘에서 많은 데이터를 사용하면 비슷비슷한 성능을 나타냅니다
        - ![performanceGraph](http://www.holehouse.org/mlclass/17_Large_Scale_Machine_Learning_files/Image.png)
        - 그래서 large dataset이 학습에 좋다는 겁니다
    - 그러나 큰 데이터셋은 큰 계산비용이 따릅니다
### Learning with large datasets
- m(data) = 100,000,000 라고 합시다
    - 비현실적이지 않고 꽤나 현실적인 숫자입니다
    - 이걸로 logistic regression model을 학습시켜봅시다
    - ![costFunction](http://www.holehouse.org/mlclass/17_Large_Scale_Machine_Learning_files/Image%20[1].png)
        - gradient descent를 하는 한스텝마다 100,000,000개를 더해야합니다
- 이것을 계산하지 않기 위해서 더 효율적인 방법을 생각해봅시다
    - 다른 접근
    - 위와 같은 합을 사용하지않는 optimizing
- 첫 번째로 할 수 있는 것은 100,000,000개의 예가 아닌 1000개의 예만 사용하는 겁니다
    - 몇개만 랜덤으로 선택하기
    - 잘 동작하도록 만들 수 있을까요?
        - 종종 그럴 수 있습니다
- 작은 샘플로 잘 동작하는지 확인해보기 위해서 training set 크기에 따른 error 플롯을 봅시다!
    - ![high_variance_problem](http://www.holehouse.org/mlclass/17_Large_Scale_Machine_Learning_files/Image%20[2].png)
        - 위는 high variance problem처럼 보입니다! 더 많은 data set이 위를 해결해줄 것입니다
    - ![high_bias_problem](http://www.holehouse.org/mlclass/17_Large_Scale_Machine_Learning_files/Image%20[3].png)
        - 더 많은 데이터셋이 도움이 되진 않습니다
        - feature를 더 추가하거나, hidden unit을 더 추가하세요!(히든 유닛은 nn일때만)
## Stochastic Gradient Descent
- linear regression을 이용하여 Stochastic Gradient Descent를 설명해보겠습니다
    - Logistic regression, Neural network 등에서도 사용할 수 있습니다
- 만약 m(example set)이 너무 많으면 Gradient Descent를 계산하는데 너무 많은 시간이 걸립니다
- 우리가 지금까지 말한 Gradient Descent를 **batch gradient descent**라고 합니다.
    - 큰 data set에서는 효율적이지 못합니다
### Stochastic gradient descent
- cost function을 조금 다르게 정의해봅시다
    - ![costFucntion](http://www.holehouse.org/mlclass/17_Large_Scale_Machine_Learning_files/Image%20[9].png)
    - 이 함수는 특정 예(x<sup>i</sup>, y<sup>i</sup>)에 대한 &Theta;의 cost를 나타냅니다
- ![train](http://www.holehouse.org/mlclass/17_Large_Scale_Machine_Learning_files/Image%20[10].png)
    - batch gradient descent cost function과 같은 식
- 확률적 경사하강법의 동작
    1. Randomly shuffle
        - training examples를 무작위로 섞습니다
    2. Algorithm body
        - ![body](http://www.holehouse.org/mlclass/17_Large_Scale_Machine_Learning_files/Image%20[12].png)
- random shuffle을 함으로써 data가 랜덤으로 정렬되어있다는 것을 확신하고, 그럼으로써 그 순간에(예제) 편향되지 않도록 해주는 것을 의미합니다
- 확률적 경사하강법은 배치 경사하강법과 비슷하지만, 모든 m 예제들을 다 더할때까지 기다리는 것이 아니라, 한 예제만 취해서 parameter들을 미리 업데이트하는 과정을 진행해놓는 것입니다.
    - 데이터를 통해 매 step마다 parameter를 업데이트 하는 것입니다!
- batch gardient descent
    - ![batch_GD](http://www.holehouse.org/mlclass/17_Large_Scale_Machine_Learning_files/Image%20[15].png)
- ![stochastic_GD](http://www.holehouse.org/mlclass/17_Large_Scale_Machine_Learning_files/Image%20[16].png)
    - 확률적 경사하강법은 모든 스텝에 대해 더 빠르지만, 각 iteration마다 한 예제에 fitting 됩니다
    - 일반적으로 global minimum을 향해 움직이지만 늘 그런 것은 아닙니다
- 구현에 대한 참고 사항
    - 한 1~10번정도 반복해야합니다
    - 정말정말 큰 데이터셋을 갖고있다면 한번만 시행해도 모델은 완벽해져있을 것입니다

## Mini Batch Gradient Descent
- Mini Batch Gradient Descent는 stochastic gradient descent보다 더 빨리 도달할 수 있는 추가적인 접근 방식입니다
- 요약
    1. Batch gradient descent : 각 iteration마다 모든 예제 m을 사용
    2. Stochastic gradient desent : 각 iteration마다 1개의 예제를 사용
    3. Mini batch gardient descent : 각 iteration마다 b개의 예제를 사용
        - b : mini-batch-size
- batch size가 좀 작아졌다는 것빼고는 똑같습니다
    - 일반적으로 2~100(아마도 10개)
    - 만약 10개면, 10가지 예제로 경사하강법 진행

- Mini batch algorithm
    - ![algorhith](http://www.holehouse.org/mlclass/17_Large_Scale_Machine_Learning_files/Image%20[17].png)

- Mini batch gradient descent를 사용해야하는 이유
    - 벡터로 구현 가능
    - 더 효율적임
    - 병렬적으로 처리 가능(한번에 10개씩!)
    - b개에 예제에 parameter들이 최적화되지만 그래도 효율적임

## Stochastic gradient descent convergence
- 이제 확률적 경사하강법에 대해 알았습니다.
    - 위 과정이 다 끝났는지 어떻게 확인하나요?
    - learning rate(&alpha;)를 어떻게 설정하나요?

### check for covergence
- ![costFunction](http://www.holehouse.org/mlclass/17_Large_Scale_Machine_Learning_files/Image%20[18].png)
    - 한 예제에서의 squared error의 1/2한 것이 cost function
- (x<sup>i</sup>, y<sup>i</sup>) 예제에 대해 알고리즘이 실행되고 있지만, &Theta;가 업데이트 되기 전에 cost(&Theta, (x<sup>i</sup>, y<sup>i</sup>))에 대해서 계산이 되어야합니다
    - &Theta;를 업데이트 전에 이것을 계산을 해야합니다
    - 업데이트를 한 후 예제를 돌리면 이전 모델보다 비교적 더 수행이 잘 될 것이기 때문입니다.
- 수렴을 확인하기 위해 1000번의 iteration을 반복할때마다 그 이전 1000개의 예제를 plotting 해봅시다
    - ![ploting](http://www.holehouse.org/mlclass/17_Large_Scale_Machine_Learning_files/Image%20[19].png)
    - 이러면 학습이 잘 된 것입니다!
- 더 작은 learning rate를 쓰면 더 좋은 결과를 얻을 수도 있습니다
    - ![plotting2](http://www.holehouse.org/mlclass/17_Large_Scale_Machine_Learning_files/Image%20[20].png)
    - 왜냐면 parameter가 global minimum근처에서 진동하기 때문입니다
- 만약 1000개가 아닌 5000개의 예제를 사용하면, curve가 더 부드러워집니다.
    - ![smooth](http://www.holehouse.org/mlclass/17_Large_Scale_Machine_Learning_files/Image%20[21].png)
    - 때로는 이런 모양을 볼 수도 있습니다
    - ![smooth2](http://www.holehouse.org/mlclass/17_Large_Scale_Machine_Learning_files/Image%20[22].png)
    - 이렇게 보면 감소하지 않는 것처럼 보일 수 있습니다
    - 만약 예제 수를 늘린다면 일반적인 감소 trend를 볼 수 있을 것입니다
    - 예를 늘려도 파란색처럼 보일 수 있습니다
- ![example](http://www.holehouse.org/mlclass/17_Large_Scale_Machine_Learning_files/Image%20[23].png)
    - 이런식으로 증가하는 모양이라면, learning rate를 줄이면 됩니다

### Learning rate
- 위를 통해 확률적 경사하강법이 우리가 원하던 minimum으로 갈 수 있도록 도와준다는 것을 알았습니다
    - 대부분의 경우에서 learning rate는 일정합니다
- 하지만 만약 minimum으로 수렴하고싶다면 조금씩 learning rate를 줄일 수 있습니다
    - 클래식한 방법은 아래처럼 계산하는 것입니다
    - &alpha; = const1/(iterationNumber + const2)
    - 이러면 어딘가로 수렴할 수 있습니다!
        - const1과 const2를 이것을 정의해야합니다
    - 만약 parameter들을 잘 튜닝한다면 아래와 같이 할 수 있습니다
    - ![example](http://www.holehouse.org/mlclass/17_Large_Scale_Machine_Learning_files/Image%20[24].png) 

## Map reduce and data parallelism
- stochastic gardient descent에 대해서 배워봤습니다
    - 그러나 어떤 예는 한 컴퓨터에서 돌리기엔 너무 클 수 있습니다
    - **Map Reduce**에 대해서 배워봅시다!
- Map reduce example
    - batch gardient descent를 사용하고싶습니다
    - ![batch_gradient_descent](http://www.holehouse.org/mlclass/17_Large_Scale_Machine_Learning_files/Image%20[26].png)
    - m이 400이라고 가정합시다
        - m이 커질수록 계산비용이 커집니다
    - training set을 4조각으로 쪼개봅시다
    - Machine 1: (x<sup>1</sup>, y<sup>1</sup>), ..., (x<sup>100</sup>, y<sup>100</sup>)을 사용합니다
    - 4분의 1개중 첫번째 training set을 사용합니다
    - 첫번째 100개를 더합시다
    - ![example1](http://www.holehouse.org/mlclass/17_Large_Scale_Machine_Learning_files/Image%20[27].png)
    - Machine2: (x<sup>101</sup>, y<sup>101</sup>), ..., (x<sup>200</sup>, y<sup>200</sup>)을 사용합니다.
    - Machine3: ...
    - Machine4: ...
    - 이렇게 함으로써 4개의 temp value를 얻었고 각 machine들이 1/4만큼 일을 끝냈습니다
    - 이 teamp variables을 얻으면...
        - master server로 전송
        - 다시 다 모읍니다
        - &Theta;를 업데이트
        - ![update](http://www.holehouse.org/mlclass/17_Large_Scale_Machine_Learning_files/Image%20[29].png)
        - 원래 배치 경사하강법 알고리즘과 같습니다!
- 더 일반적으로 map reduce를 아래와 같이 표현합니다
    - ![show](http://www.holehouse.org/mlclass/17_Large_Scale_Machine_Learning_files/Image%20[30].png)
- 이 경사하강법에서 많은 일을 차지하는 것은 summation입니다
    - 이제 기계가 4대가 나눠서하니 속도가 1/4로 줄어듭니다
    - 사실 network latency 등으로 좀 느릴 수 있는데 그래도 오히려 좋습니다!
- 중요한 것은...
    - training set의 sum computing 함수로 표현될 수 있나요? ==> 그럼요!
    - 많은 알고리즘에서 사용할 수 있습니다!

### Hadoop
- 하둡은 오픈소스 Map Reduce 구현입니다!