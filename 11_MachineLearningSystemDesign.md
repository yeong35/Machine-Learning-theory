# Machine learning system design

## Prioritizing Wat to Work On
- **spam mail을 걸러내는 모델을 만든다고 가정하자!**
- 받은 mail에 모든 word에 스팸에 해당할 것 같은 단어에 1, 아닌 단어에 0을 준 후 이것들을 vector로 구성
- 정확도를 어떻게 높일까?
    - 많은 데이터 수집
    - email routing information에 기반한 정교한 기능 개발
    - 메시지 본문을 분석하는 특징 기능 개발
    - 철자가 틀린 단어를 찾아내는 알고리즘 개발
    - 연구 그룹들은 종종 위에 중 한 옵션에 무작위로 집중함
- 내가 적용할 것들
    - 데이터 많이 모으기
    - 특징 만들기
    - 여러가지 방법으로 내 input 구성하는 알고리즘 만들기(misspelling으로 스팸을 찾는 것)

## Error Analysis
- machine learning 문제를 풀기위해 추천하는 방법은..
    - 쉬운 algorithm을 통해 시작하기 그리고 cross validation data로 테스트하기
    - learning curves로 데이터를 늘릴지 feature를 늘릴지 다른걸할지 결정하기.
    - cross validation set과 같은 것들로 example들의 error 평가하기

## Error Metrics for Skewed Classes
- True positive (1이라고 생각했는데 진짜 1임)
- False positive (1이라고 생각했는데 0임)
- True negative (0이라고 생각했는데 진짜 0임)
- False negative (0이라고 생각했는데 1임)
    - ![PrecisionAndRecall](https://blog.nillsf.com/wp-content/uploads/2020/05/image-36.png)
- Precision
    - 알고리즘이 얼마나 자주 허위 경보(false alarm)을 울리는지 검증
    - = true positive/(true positive + false positive)
    - 1에 가까울 수록 좋음!
- Recall
    - 알고리즘이 얼마나 예민한지 검증
    - true positives/(true positive + false negative)
    - 1에 가까울수록 좋음!

## Trading off precision and recall
- 만약, 0과 1을 나누는 threshold를 너무 높게 잡는다면 true positive에는 자신있어지지만 recall의 값은 낮아지게된다
- threshold를 낮춘다면 higher recall을 가질 수 있지만 precision은 낮아진다
- ![recallAndPrecision](http://www.holehouse.org/mlclass/11_Machine_Learning_System_Design_files/Image%20[2].png)
    - classifier의 detail에 따라 위 curve는 좀 달라질 수 있음
- ![precisionRecallTable](http://www.holehouse.org/mlclass/11_Machine_Learning_System_Design_files/Image%20[3].png)
- 위와 같은 표가 있을때, 3개 중 어떤 알고리즘이 제일 좋을까?
- **F<sub>1</sub>Score(fscore)** 를 사용하자
    - = 2*(Precision*Recall/(Precision+Recall))
    - Fscore는 precision과 recall의 평균을 구하는 것과 같으며 낮은 값에 더욱 높은 가중치를 부여한다
- threshhold를 자동으로 정하는 방법은 다양한 threshold로 학습시킨후 crossvalidation set으로 평가하기
- 그 후 fscore가 가장 높은 걸 pick!

## Data for machine learning
- ![algorithmAndAccuracy](http://www.holehouse.org/mlclass/11_Machine_Learning_System_Design_files/Image%20[4].png)
- 알고리즘은 비슷한 퍼포먼스를 냄
- training set size가 증가하면 정확도도 증가됨
    - 많은 데이터가 도움이 된단 얘기
- 정리
    - x가 y를 예측하기에 충분한 정보를 주면, 많은 데이터가 도움이 될가용
    - 많은 feature와 hidden unit이 있는 neural network거나, 많은 parameter를 가진 logistic regression알고리즘은 완전 좋다
        - 낮은 bias를 가짐
    - 작은 training set 사용!
        - 그러면 training error도 작겠지
    - 큰 training set사용!
        - trining error랑 test error랑 비슷해짐
        - 복잡한 알고리즘에 더 잘 어울림
        - test set error가 더 작아질 것
    - 낮은 bias를 갖고싶어! -> 복잡한 알고리즘 사용하기
    - 낮은 variancee를 갖고싶어! -> 큰 training set 사용하기