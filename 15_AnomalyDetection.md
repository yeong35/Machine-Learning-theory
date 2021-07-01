# 15. Anomaly Detection
## Anomaly detection - problem motivation
- machine learning application에서 널리 사용됩니다.
    - 비지도 학습 문제의 해결책으로도 사용 가능
    - 그러나 지도학습의 측면도 갖고 있습니다
- Anomaly detection이란?
    - 우리는 normal data를 갖고 있습니다.
    - 그러나 normal이라고 여기는 것은 우리에게 달려있다!
    - 이러한 normal data을 reference point로 사용하면서, 다른 예제들이 이상점인지 확인할 수 있습니다
- 어떻게?
    - 첫번째로, training set으로 model을 만듭니다.
        - p(x)를 사용하여 이 모델에 접근할 수 있습니다.
    - 모델이 구축된 후에는?
        - 만약 p(x<sub>test</sub>) < &epsilon; -> anomaly
        - 만약 p(x<sub>test</sub>) >= &epsilon; -> normal
        - &epsilon;은 필요/확실성에 따라 정의되는 threshold 입니다
    - ![expect](http://www.holehouse.org/mlclass/15_Anomaly_Detection_files/Image%20[3].png)
### Applications
- Fraud detection(AI RUSH 1-1과제를 여기에 적용할 수도 있을 것같다)
- 제조업
- Monitoring computers in data center

## The Gaussian distribution (optional)
- normal distribution이라고도 불림(정규 분포)
- ![normal_distribution](http://www.holehouse.org/mlclass/15_Anomaly_Detection_files/Image%20[4].png)
- x가 &mu;를 벗어날 때의 확률을 지정
- Gaussian equation
    - P(x : &mu;, &sigma;<sup>2</sup>) (x는 확률, &mu;, &sigma;<sup>2</sup>로 정해집니다.)
    - ![equation](http://www.holehouse.org/mlclass/15_Anomaly_Detection_files/Image%20[5].png)
- ![example](http://www.holehouse.org/mlclass/15_Anomaly_Detection_files/Image%20[6].png)
### Parameer estimation problem
- m개의 data set이 있다고 가정해봅시다
- 각 예제들은 실수값입니다 아래와 같이 x축에 표현할 수 있습니다.
- ![example1](http://www.holehouse.org/mlclass/15_Anomaly_Detection_files/Image%20[7].png)
- ![example2](http://www.holehouse.org/mlclass/15_Anomaly_Detection_files/Image%20[8].png)
- 정규분포로 예측하면 위와같습니다. 중앙에 위치할 확률이 높습니다.
- &mu;와 &sigma;<sup>2</sup>을 예측해보자
    - ![equation](http://www.holehouse.org/mlclass/15_Anomaly_Detection_files/Image%20[9].png)
        - 위 식은 1/m인데 1/(m-1)랑 큰차이 없으니 아무거나 쓰세요
## Anomaly detection algorithm
- unlabeled training set이 m개 있다고 합시다
    - Data = {x<sup>1</sup>, ..., x<sup>m</sup>}
        - 각 예제들은 n-dimensional vector, n개의 특징을 가지고 있는 것!
    - data set으로부터 만들어진 model P(x)
        - p(x) = ( p(x<sub>1</sub>; &mu;<sub>1</sub>, &sigma;<sub>1</sub><sup>2</sup>)* p(x<sub>2</sub>; &mu;<sub>2</sub>, &sigma;<sub>2</sub><sup>2</sup>) * ... * p(x<sub>n</sub>; &mu;<sub>n</sub>, &sigma;<sub>n</sub><sup>2</sup>) )
        - 각 특징들의 확률을 곱합시다
            - 각 특징들이 정규분포를 따른다고 가정하고 모델을 모델링합시다
            - p(x<sub>i</sub>; &mu;<sub>i</sub>, &sigma;<sub>i</sub><sup>2</sup>)
                - &mu;<sub>i</sub>, &sigma;<sub>i</sub><sup>2</sup>가 주어졌을 때 x<sub>i</sub> 특징의 확률입니다
    - side comment
        - 위 식은 feature들이 독립적이라고 가정하고 만들어졌습니다 그러나 feature들이 독립적인지 아닌지 관계없이 알고리즘은 작동됩니다
            - 너무 걱정하지 않아도 됩니다 만약 feature들이 긴밀히 연결되어 있어도 차원축소는 할 수 있을 겁니다
    - ![equation](http://www.holehouse.org/mlclass/15_Anomaly_Detection_files/Image%20[10].png)

### Algorithm
- ![Algorithm](http://www.holehouse.org/mlclass/15_Anomaly_Detection_files/Image%20[11].png)
1. Chose features
    - 너무 크거나, 너무 작은 이상점을 식별하는데 도움이 될만한 특징을 찾아보기
    - 일반적으로,  일반 특징을 설명하는 feature를 선택합니다.
    - 이것들이 독특한건 아니고 단지 합리적인 feature vector를 택하는 아이디어
2. Fit parameters
    - 각 example에 &mu;<sub>i</sub>, &sigma;<sub>i</sub><sup>2</sup> parameter를 결정합니다
        - 조금의 오류가 있을 순 있습니다. 실제로는 1~n개에 대한 매개변수 계산입니다
    - 각 feature에 대한 standard deviation(표준 편차)와 mean을 계산해야합니다
    - loop보다 vectorized implemetation 이용하기
3. compute P(x)
- 표시된 공식을 계산하기(여기서는 Gaussian probability)
- 만약 수가 너무작다면 normal일 가능석은 매우 낮습니다.

### Anomaly detection example
- ![example1](http://www.holehouse.org/mlclass/15_Anomaly_Detection_files/Image%20[12].png)
- ![example2](http://www.holehouse.org/mlclass/15_Anomaly_Detection_files/Image%20[13].png)
- ![example3](http://www.holehouse.org/mlclass/15_Anomaly_Detection_files/Image%20[14].png)
## Developing and evaluating and anomaly detection system
- 만들어진 알고리즘을 어떻게 평가할까?
- 알고리즘을 변경했을때 변경으로인해 성능이 더 좋아졌는지, 안좋아졌는지 숫자로 확인할 수 있다면 더 쉽게 알고리즘을 평가할 수 있을 것입니다!
- 이상탐지 시스템을 빠르게 만들기 위해, 알고리즘을 평가하는 것이 도움이 될 것입니다.
- 일단, label이 붙은 데이터들이 있다고 가정합시다
    - 지금까지는 unlabel 데이터로 학습을 해왔습니다
- engine 생성라인의 예시를 들어보자!
    - non-anomalous -> y = 0
    - anomalous -> y = 1
    - training set은 일반 예제들의 집합입니다
        - anomalous data가 적어도 괜찮습니다
    - 다음으로 아래를 정의해줍시다
        - Cross Validation set
        - Test Set
        - 위의 두가지 모두 anomalous examples를 포함한다고 가정합시다
    - Training set, CV set, Test set을 6:2:2 정도로 나눕니다
        - 6:4:0으로 나누기도 합니다 (근데 이러면 별로 안좋으니까 CV랑 test로 나눠주세요)
    - 알고리즘 평가
        - training set {x<sup>1</sup>, ..., x<sup>m</sup>}
            - 이걸로 model을 학습시켜봅시다
        - CV랑 test도 돌립시다
            - y = 1, 만약 p(x) < epsilon (anomalous)
            - y = 0, 만약 p(x) >= epsilon (normal)
     - 알고리즘이 anomalous를 예측할때를 생각하면.. 
        - 우리는 label을 갖고있으니 anomalous를 확인할 수 있습니다.
        - 지도학습처럼 만들 수 있습니다.
- 뭐가 평가에 좋은 방법이냐면...
    - y = 1인 경우를 찾기 힘들기 때문에
    - true positives, false positive, fasle negative, true negative 계산하기
    - prevision, recal 계산하기
    - F1-score 계산하기
- epsilon
    - 비정상 값을 표시할 threshold
    - 만약 CV set을 갖고있다면, epsilon 값이 어떻게 변하는지 볼 수 있을 것입니다.
        - CV 점수가 가장 커지는 epsilon을 선택하세요
    - cross validation을 이용해서 알고리즘을 평가하세요
    - 마지막으로 test set으로 알고리즘 평가하기

## Anomaly detection vs supervised learning

- 언제 supervised learning를 쓸 지, anomal detection을 쓸 지 배워봅시다

### Anomaly detection

1. positive examples가 엄청 적을 때

    - CV랑 test set의 positive examples를 저장

    - anomaly detection을 사용할지 고민

    - "학습"에 사용할 positive examples가 충분하지 않을때

2. negative examples가 너무 많을 때

    -  p(x)를 학습할때 negative examples를 사용하기

    - negative example만 필요함

3. 많은 타입의 anomalites

    - anomalies가 서로서로 많이 다르다면 positive로부터 알고리즘을 학습시키는데 어렵습니다

 

### Supervised learning

- 이상적으로 positive and negative example이 많을 때

    - 같은 형식으로 많은 anomalies가 나타날 때

- 예시

    - Email, SPAM classification

    - Weather prediction

    - Cancer classification

 

## Choosing features to use

- 어떤 특징을 사용할지 정하는 것이 중요합니다

- Non-Gaussian features

    - 데이터가 Gaussian description인지 확인합니다

    - ![non-gaussian](http://www.holehouse.org/mlclass/15_Anomaly_Detection_files/Image%20[15].png)

    - 변화를 주어서 Gaussian처럼 보이게 합니다(log로 바꾼다는 등..)

    - ![gaussian](http://www.holehouse.org/mlclass/15_Anomaly_Detection_files/Image%20[16].png) 

    - log(x<sub>1</sub>+c), x<sup>1/2</sup>, x<sup>1/3</sup>등을 사용할 수 있습니다

### Error analysis for anomaly detection

- supervised learning error analysis procedure랑 비슷합니다

    - CV set을 사용하여 알고리즘 돌리기

    - 후 뭐가 틀렸는지 보기

    - 왜 알고리즘이 이 example에 대해 틀렸는지 이해하기 위해 새로운 feature를 이용하여 개발하기

## Multivariate Gaussian distribution
- non-multivariate Gaussian distribution anomaly detection이 실패했을때 anomaly detection을 할 수 있는 약간 다른 기법입니다.
    - 아래는 unlabeled data입니다.
    - ![unlabeledData](http://www.holehouse.org/mlclass/15_Anomaly_Detection_files/Image%20[18].png)
    - 아래같은 초록점이 이상점이라고 합시다
    - ![example11](http://www.holehouse.org/mlclass/15_Anomaly_Detection_files/Image%20[19].png)
    - 위의 초록점은 단변량 분포에서는 acceptable limits에 들어오지만, 함께봤을땐 아닙니다
    - 그러나 이런 feature들을 한번에 보면 안됩니다.
    - ![circle](http://www.holehouse.org/mlclass/15_Anomaly_Detection_files/Image%20[20].png)
    - 우리 function이 동짐원에서의 확률 예측은 위에 두개의 빨간 동그라미와 같은 확률을 갖기 때문입니다
    - 녹색 예제를 outlier긴 하지만 의미는 이해하지 못합니다
### Multivariate Caussian distribution model
- 위와같은것을 극복하기 위해 multivariate Gaussian distribution을 개발해봅시다
    - Model p(x)는 각 feature들을 분리하지않고 한번에 모델링합니다
        - 새로운 함수의 새 parameter
            - &mu; : n dimensional vector
            - &Sigma; : [n x n] matrix - covariance matrix
- multivariate Gaussian distribution의 식은 아래와 같습니다
    - ![multivariateGaussianDistribution](http://www.holehouse.org/mlclass/15_Anomaly_Detection_files/Image%20[21].png)
    - NB는 언제든 볼 수 있어서 따로 저장하지 않습니다
    - 위 식은 무엇을 의미하는가?
        - |&Sigma;| = &Sigma;의 절댓값 MATLAB으로 det(sigma)로 가능
- 더 중요한 것은 p(x)가 어떻게 생겼는가
    - 2D example
    - ![2Dexample](http://www.holehouse.org/mlclass/15_Anomaly_Detection_files/Image%20[23].png)
        - sigma는 종종 identity matrix라고도 불립니다
    - ![2Dexample1](http://www.holehouse.org/mlclass/15_Anomaly_Detection_files/Image%20[24].png)
        - z축은 p(x)가 계산해낸 값
    - 만약 sigma값이 바뀐다면..?
        - ![2Dexample3](http://www.holehouse.org/mlclass/15_Anomaly_Detection_files/Image%20[25].png)
        - 폭이 감소하고 높이가 증가되었습니다
        - sigma가 바뀌면 그래프의 모양이 바뀝니다
    - 이런 것을 사용함으로써, data의 shape를 더 잘 맞도록 정의할수있습니다(모든 dimension이 대칭이라고 가정하지않고)
    - ![2Dexample4](http://www.holehouse.org/mlclass/15_Anomaly_Detection_files/Image%20[28].png)
    - 3번째 예제는 강한 양의 관계를 보여줍니다!
        - 만약 역대각선의 성분들을 음수로하면 음의 상관관계를 표시할 수도 있습니다
    - &mu;를 움직임으로써 peak를 이동시킬수도 있습니다
## Applying multivariate Gaussian distribution to anomaly detection
- 위에 모델링 할 수 있는 몇개의 예를 보았습니다
    - 지금부터는 이것을 anomaly detection algorithm에 적용해보겠습니다
- 아까 말한 것처럼 multivariate Gaussian modeling은 아래와 같은 식을 사용합니다
    - ![multivariateGaussian](http://www.holehouse.org/mlclass/15_Anomaly_Detection_files/Image%20[29].png)
        - &mu; : n dimensional vector
        - &Sigma; : [n x n] matrix - covariance matrix
    - ![&mu;](http://www.holehouse.org/mlclass/15_Anomaly_Detection_files/Image%20[30].png)
    - ![&sigma;](http://www.holehouse.org/mlclass/15_Anomaly_Detection_files/Image%20[31].png)
    - 두 식을 사용하여 parameter를 얻을 수 있습니다
### Anomaly detection algorithm with multivariate Gaussian distribution
1. Fit model (데이터 셋을 사용하고 위 식을 사용하여 &mu;와 &Sigma;를 계산합니다)
2. 아래는 새로 주어진 예제입니다(x<sub>test</sub>)
    - ![xTest](http://www.holehouse.org/mlclass/15_Anomaly_Detection_files/Image%20[32].png)
    - 아래의 식(multivariate distribution)을 사용하여 p(x)를 계산합니다
    - ![multivariateDistribution](http://www.holehouse.org/mlclass/15_Anomaly_Detection_files/Image%20[33].png)
3. &epsilon;과 value 비교하기
    - 만약 p(x<sub>test</sub>) < &epsilon; --> anomaly
    - 만약 p(x<sub>test</sub>) >= &epsilon; --> normal
    - 만약 multivariate Gaussian model을 우리의 data에 적용하면...
    - ![model](http://www.holehouse.org/mlclass/15_Anomaly_Detection_files/Image%20[34].png)
        - normal Gaussian model은 multivariate Gaussian의 축이 정렬된 모델로 multivariate Gaussian의 특별한 경우라고 볼 수 있습니다
        - ![multivariateDistribution2](http://www.holehouse.org/mlclass/15_Anomaly_Detection_files/Image%20[35].png)
        - 만약 위처럼 sigma가 identity matrix라면 original이랑 모델이 똑같습니다]
## Original model vs Multivariate Gaussian
1. Original Gaussian model
    - 더 자주 쓰입니다
    - x<sub>1</sub>, x<sub>2</sub>의 비정상적인 조합에서 anomalies를 포착하기위해, feature를 수동으로 생성해야합니다.
        - 그래서 추가적인 feature가 필요한데, 그것이 뭔지는 확실하지 않습니다
            - 문제에 대한 예상을 미래의 anomalies의 예상에 사용하기에는 risk가 있습니다
            - 당신이 잡으려는 오류랑 잡힌 오류랑은 조금 다를 것입니다
    - 계산비용이 적습니다
    - 큰 feature vector에 더 잘 맞을 것입니다
        - 만약 n=100000이면, original model이 잘 돌아갈 것입니다
    - 작은 training set에서도 잘 돌아갑니다
        - 한 50~100개 정도
2. Multivariate Gaussian model
    - 비교적 덜 자주 쓰입니다
    - correlation feature를 캡쳐할 수 있습니다
        - 또다른 value를 만들지 않아도 됩니다
    - 계산효율이 낮습니다
        - [n x n] matrix를 계산해야합니다
        - 너무 많은 feature는 좋지 않습니다 (계산비용이 커지기 때문에)
        - n = 100000은... 좋지않아요
    - m(예제) > n(feature) 때만 쓰세요
    - 만약 matrix가 non-invertible이라며면 두가지 이유중 하나일 수 있습니다
        1. m < n
        2. 중복된 feature
