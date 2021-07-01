# 16 Recommender Systems

## Recommender systems - introduction
- n<sub>u</sub> : 유저 수
- n<sub>m</sub> : 영화 수(예시)
- r(i, j) - j 유저가 i 영화에 평가했으면 1
- y<sup>(i, j)</sup> : 어떤 유저 j가 i 영화에 준 평점
## Content based recommendation
- 각 영화에 대한 정도를 측정하는 feature가 있습니다
    - Romance(x<sub>1</sub>)
    - Action(x<sub>2</sub>)
- ![example](http://www.holehouse.org/mlclass/16_Recommender_Systems_files/Image%20[1].png)
- 우리가 이러한 특징을 가지고 있다면, 각 영화들은 feature vector에 의해 추천될 수 있습니다
    - 각 영화에 x<sub>0</sub>을 추가해주면 x<sup>1</sup>(love at last)는 아래와 같을 것입니다
    - ![loveAtLast](http://www.holehouse.org/mlclass/16_Recommender_Systems_files/Image%20[2].png)
    - 일단 우리는 아래와 같은 데이터 set을 가지고있습니다(영화가 5개니까..)
    - {x<sub>1</sub>, x<sub>2</sub>, x<sub>3</sub>, x<sub>4</sub>, x<sub>5</sub>}
        - 각 x들의 feature 개수는 n=2(x<sub>0</sub>는 세지 않습니다)
- 각 사용자들의 평가를 linear regression problem으로 다룰 수 있습니다
    - 각 uesr j에게 parameter vector를 학습시킬 수 있습니다
    - 그후 user j가 영화 i를 좋아할 지 예측시킵니다
        - (&Theta;<sup>j</sup>)<sup>T</sup>x<sup>i</sup> = star
    - M<sup>j</sup> : user j가 평가한 영화의 개수

### How do we learn(&Theta;<sup>j</sup>)
- 적용 시 데이터에 표시된 값만큼 가까운 값을 제공하는 일부 파라미터를 생성합니다
    - ![equation1](http://www.holehouse.org/mlclass/16_Recommender_Systems_files/Image%20[5].png)
- r(i, j) = 1일 때, i(사용자가 평가한 모든 영화)의 합
- linear regression의 least-squared error와 비슷합니다
- 우리는 아래와 같은 식을 사용해서 정규화할수도 있습니다
- ![regularization](http://www.holehouse.org/mlclass/16_Recommender_Systems_files/Image%20[6].png)
    - 정규화는 k=1부터 n까지만! 따라서 (&Theta;<sup>j</sup>)는 n+1 feature vector입니다.
- 이렇게하면 합리적인 값을 얻을 수 있습니다
- 좀 더 분명히하기위해 m<sup>j</sup>를 없앨 수 있습니다(그냥 상수라 별 영향안끼침)
    - ![regularization2](http://www.holehouse.org/mlclass/16_Recommender_Systems_files/Image%20[7].png)
    - 그러나 우리는 모든 유저에 대해 parameter를 학습시키고싶습니다 따라서 우리는 몇 summation term을 추가합니다(모든 유저에 대해 (&Theta;<sup>j</sup>))
    - ![everyUserRegularization](http://www.holehouse.org/mlclass/16_Recommender_Systems_files/Image%20[8].png)
    - 각 (&Theta;<sup>j</sup>)에 위와같이 실행한다면, 각 사용자에 대한 파라미터를 얻을 수 있습니다
        - 이것이 우리의 최적화 목표입니다! -> J(&Theta;<sup>1</sup>, ..., &Theta;<sup>nu</sup>)
- 다른말로는, 아래와같은 gradient descent를 통해 최소화 합니다
    - ![gradientDescent](http://www.holehouse.org/mlclass/16_Recommender_Systems_files/Image%20[9].png)
    - 전에 배운 gradient descent랑은 조금 다릅니다
        - k = 0과 k != 0 versions
        - 가운데 term은 아래와같이 정의할 수 있습니다
        - ![middleTerm](http://www.holehouse.org/mlclass/16_Recommender_Systems_files/Image%20[10].png)
        - linear regression과의 차이점
            - 1/m term이 없음
            - 그거 빼곤 다 비슷
- 이러한 접근을 content-based 접근이라고 합니다 왜냐면 우리는 content와 관련있는 feature를 통해 사용자에게 매력적인 것을 식별할 수 있다고 가정하기 때문입니다
- 근데 이러한 feature를 사용할 수 없는 경우가 많습니다
## Collaborattive filtering - overview
- collaborative filtering algorithm은 흥미로운 특징을 갖고있습니다(feature를 학습할 수 있습니다)
    - 어떤 feature가 학습에 필요한지 배울 수 있습니다
- 위의 예에선 액션과 로맨스만 다뤘지만 현실세계에서는 더 많은 feature가 필요할 수 있습니다
- 따라서 문제를 바꾸고 영화에 관련된 feature를 아무것도 모른다고 가정합시다
- ![example](http://www.holehouse.org/mlclass/16_Recommender_Systems_files/Image%20[11].png)
    - 또다른 가정을 세워봅시다
        - 각 유저들에게 어떤 것을 얼마나 좋아하는지 물어봤습니다
        - Romantic films, Action films
        - 아래와 같은 parameter set을 얻게되었습니다
        - ![parameterSet](http://www.holehouse.org/mlclass/16_Recommender_Systems_files/Image%20[12].png)
        - 1번과 2번은 로맨스를 좋아하지만 액션은 싫어하고 2번과 3번은 액션은 좋아하지만 로맨스는 싫어합니다
- 이렇게 물어봄으로써 missing value를 추론할 수 있습니다
    - 1과 2는 로맨스를 좋아하고 2, 3은 로맨스를 싫어하니까 1번영화는 정확히 로맨스 영화라는 것을 알 수 있다
- 근데 우리가 진짜 하고싶은것은
    - (&Theta;<sup>1</sup>)<sup>T</sup>x<sup>1</sup>는 5, (&Theta;<sup>2</sup>)<sup>T</sup>x<sup>1</sup>는 5, (&Theta;<sup>3</sup>)<sup>T</sup>x<sup>1</sup>는 0, (&Theta;<sup>4</sup>)<sup>T</sup>x<sup>1</sup>는 0이 되도록 하는 것입니다.
    - 아래와 같은 x<sup>1</sup>으로부터 위처러 만드는 것이 목푭니다
    - ![x](http://www.holehouse.org/mlclass/16_Recommender_Systems_files/Image%20[13].png)
    - 동일한 접근 방식을 사용하여 다른 여화나 나머지 feature vector를 결정할 수 있어야 합니다!
### Formalizing the collaborative filtering problem
- 좀 더 formal하게 설명해봅시다
- (&Theta;<sup>1</sup>, ..., &Theta;<sup>nu</sup>)가 있다고 합시다(각 유저들의 선호 vector parameter)
- 영화와 관련된 parameter vector를 식별하기 위해 optimization function을 최적화해야합니다
- ![minimize](http://www.holehouse.org/mlclass/16_Recommender_Systems_files/Image%20[14].png)
- 그래서 영화 i에 대한 데이터가 있는 곳에 대한 모든 index j를 더합니다
- 위에서처럼 이 등식으로 한 영화에 대한 feature를 배울 수 있는 방법을 제공합니다
    - 모든 영화에 대한 feature를 학습하기를 원합니다. 따라서 summation term이 더 필요합니다
### How does this work with the previous recommendation system
- Content based recommendation systems
    - 만약 영화 rating에 관한 feature set이 있다면, 유저에 대한 선호도를 알 수 있다
- Now
    - 유저 선호도를 갖고있다면, 영화의 feature를 결정할 수 있다
- 닭이 먼저냐 치킨이 먼저냐 하는 차이와 비슷함
- 내가 할 수 있는 건...
    - &Theta;값을 무작위로 추측하기
    - collaborative filtering을 사용하여 x 생성하기
    - &Theta;를 향상시키기 위해서 content based recommendation 사용하기
    - x를 향상시키기 위해 사용하기
    - 기타등등..
- 위의 과정은..
    - 알고리즘이 합리적인 parameter set에 수렴하도록 돕습니다
    - 이건 collaborative filtering이라고 합니다
## Collaborative filtering Algorithm
## Vectorization: Low rank matrix factorization
## Implementation detail: Mean Normalization
