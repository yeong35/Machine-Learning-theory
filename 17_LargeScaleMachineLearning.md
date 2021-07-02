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
- 