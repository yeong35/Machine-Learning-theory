# Advice for applying Machine Learning

## hypothesis 평가하기
- 뭔가 우리 예상과 달리 error가 좀 높다면...
    - training set 늘리기
    - features 줄이기
    - features 늘리기
    - 다항식 feature 사용하기
    - &lambda; 줄이거나 늘리기 
- **error가 낮아도 정확도가 높지않을 수 있다. 그래서 hypothesis를 평가해야한다!**
    - data를 70%정도는 training set, 30%는 test set으로 사용
- error는 아래와 같이 정의
    - ![errorDefine](http://www.holehouse.org/mlclass/10_Advice_for_applying_machine_learning_files/Image%20[4].png)
- test error 비율 : 모든 error값/test set의 개수
    - ![testErrorDefine](http://www.holehouse.org/mlclass/10_Advice_for_applying_machine_learning_files/Image%20[5].png)

## Model selection and training validation test sets
- 만약 위처럼 모든 데이터 중 앞에 70%는 train, 나머진 test로 사용한다면 그 train, test에만 과적합될 수 있다
- 이것을 방지하기 위해 cross validation(교차검증)을 사용한다
    - ![crossValidation](https://mblogthumb-phinf.pstatic.net/MjAxOTA3MjVfMTYw/MDAxNTY0MDYxOTQxODg2.2SJCkdADPvofL7LceWnSthfefB3UvnQ2_YoRp5F2vFog.4EZrViOF41rKfovPOJJMyv7W2HKTEvfDyg92pwIIIJ4g.PNG.ckdgus1433/image.png?type=w800)

- 세 개의 방법을 사용하여 각각의 error value를 측정할 수 있습니다.
    1. 각각의 polynomial degree(1차~n차)를 사용하여 &Theta; 최적화하기
    2. cross validation set을 사용하여 가장 작은 error를 내는 polynomial degree d를 찾기
    3. test set을 사용하여 일반화 측정하기

## Diagnose bias vs variance
- 우리는 이상한 예측을 만들게 하는 것이 bias인지, variance인지 확인해야한다
- training error는 polynomial의 degree d가 커질수록 낮아지는 경향이 있다.
- cross validation error도 d가 커질수록 감소하는 경향이 있다
- High bias(underfitting) : J<sub>train</sub>(&Theta;)랑 J<sub>CV</sub>(&Theta;) 모두 높다
- High variance(overfitting) : J<sub>train</sub>(&Theta;)가 J<sub>CV</sub>(&Theta;)보다 낮다
    - ![biasVSvariance](http://www.holehouse.org/mlclass/10_Advice_for_applying_machine_learning_files/Image%20[9].png)

## Regularization and bias/variance
- &lambda;가 너무 크면 underfit(high bias), 너무 작으면 overfit(high variance)
    - ![lambdaGraph](http://www.holehouse.org/mlclass/10_Advice_for_applying_machine_learning_files/Image%20[12].png)
- &lambda;
    1. lambda list만들기 (ex. 0, 0.01, 0.02, 0.04, ..., 10.24)
    2. 다양한 degrees의 models만들기
    3. 각 lambda로  &Theta;를 학습
    4. regularization나 &lambda; 없이 학습된 &Theta;를 통해 J<sub>CV</sub>(&Theta;)를 계산
    5. 가장 낮은 error랑 cros validation error를 나타낸 &Theta;와 &lambda;을 선택!
    6. 선택된 &Theta;랑 &lambda;를 J<sub>test</sub>(&Theta;)에 적용해보기

## Learning curves
- bias가 크면
    - J<sub>train</sub>(&Theta;)
        - 처음엔 작았다가 점점 증가
        - cross validation error과 점점 가까워짐
    - J<sub>cv</sub>(&Theta;)
        - 조금만 학습한다면 엄청 클 것임...
        - 학습할수록 점점 감소할 것
- ![trainingGraph1](http://www.holehouse.org/mlclass/10_Advice_for_applying_machine_learning_files/Image%20[14].png)
- variance가 크면
    - J<sub>train</sub>(&Theta;)
        - training set이 너무 작으면 오류도 왕작을 것  
        - training set이 커짐에 따라서... J(&Theta;)은 여전히 작을 것이다 그러나 조금씩 느리게 증가할것
        - error도 여전히 작을 것
    - J<sub>cv</sub>(&Theta;)
        - training set이 중간정도있어도, error가 여전히 높은 상태로 남아있을것
        - 왜냐면 높은 variance가 모델을 일반화해후지 않기 때문이지~! 
    - training error와 validation error의 갭을 갖게된다는 것을 의미!~!~!
- ![trainingGraph2](http://www.holehouse.org/mlclass/10_Advice_for_applying_machine_learning_files/Image%20[15].png)
- 데이터가 많으면 이런것들을 도와줄수있음!~!~!

## Deciding what to do next revisited
- 많은 예제 -> high variance를 도와줌!
    - high bias를 갖는다면 좋진않음
- smaller set of features -> high variance(overfitting)를 고침!
- feature 추가 -> high bia 고침
- add polynomial terms -> high bia 고침!
- &lambda; 줄이기 -> high bias 고침!
- &lambda; 늘리기 -> high variance 고침!
- Neural Networks
    - fewer network -> underfitting, 계산량 작음
    - large network -> overfitting, 계산량 큼