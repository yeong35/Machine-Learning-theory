# 14. Dimensionality Reduction (PCA)
- PCA가 말하는 것: 데이터들을 정사영 시켜 차원을 낮춘다면
- 어떤 벡터에 데이터들을 정사영 시켜야 원래의 데이터 구조를 제일 잘 유지할 수 있을까?
## Motivation 1: Data compression
- 또다른 비지도 학습에 대해서 배워보자 - **dimensionality reduction**
### Compression
- 속도 향상 알고리즘
- 이것을 사용하여 데이터의 공간을 줄인다
- dimensionality reduction이란?
    - 우리는 많은 feature들에 대해서 모았고 이것은 아마도 내가 필요한 것보다 많을거야
    - 합리적이고 유용하게 데이터 셋을 간단하게 할 수 있을까?
- ![2Dto1D](http://www.holehouse.org/mlclass/14_Dimensionality_Reduction_files/Image%20[1].png)
    - 차원은 압축되었지만 loss가 증가될 수도 있음
- ![3Dto2D](http://www.holehouse.org/mlclass/14_Dimensionality_Reduction_files/Image%20[3].png)
    - 또다른 예제를 볼까요? 저 데이터들을 2D 그래픽에서 설명하기는 어렵지만 평면에 표현할 수 있습니다
    - 모든 점이 저 파란 트레이 안에 있다고 가정해봅시다!
    - ![3Dto2D2](http://www.holehouse.org/mlclass/14_Dimensionality_Reduction_files/Image%20[4].png)
    - x, y축을 z<sub>1</sub>, z<sub>2</sub>로 바꿔서 표현하면 평면에 표현될 수 있습니다
    - 이렇게 함으로써 3D vector를 2D vector로 줄일 수 있습니다
        - 이런 식으로 1000D를 100D로 줄일 수 있습니다
## Motivation 2: Visualization
- 높은 차원의 데이터를 시각화 하는 건 어려운 일입니다(ex) 4차원이면 어떻게 표현해야할까요..?)
    - 이것뿐만 아니라, 데이터를 더 잘 이해함으로써 알고리즘 개발도 쉬워지고
    - 데이터를 보기도 쉽고 남들에게 설명해주기도 쉽습니다!
- 만약 우리가 50D -> 2D로 만들었다고 했을때, 이 새로운 feature들에 새로운 의미를 부여하지 않고, 무엇을 의미하는지 결정해야합니다
## Principle Component Analysis(PCA): Problem Formulation
- dimensionality reduction을 할 때에는 PCA 알고리즘을 활용합니다
- PCA의 동작에 대해 알아보자
    - ![2Dto1D](http://www.holehouse.org/mlclass/14_Dimensionality_Reduction_files/Image%20[7].png)
    - 목표는 2D를 1D로 만드는 것입니다
        - 다른 말로는 한 직선에 데이터들을 정사영 시키는 것입니다!
    - ![2Dto1D](http://www.holehouse.org/mlclass/14_Dimensionality_Reduction_files/Image%20[8].png)
        - 저 파란 선을 **projection error**라고 합니다
        - 저것이 최소화되는 부분을 찾는 것이 PCA의 목적입니다(현재는 2D to 1D니까 직선을 찾는게 목표)
        - 또한, PCA를 하기 전에 데이터에 대한 mean normalization과 feature scailing을 해야합니다!
    - 더 formal하게 표현하자면
        - 우리는 projection error를 최소화할 수 있는 u<sup>(i)</sup> vector를 찾아야 합니다!
        - ![u<sup>1</sup>](http://www.holehouse.org/mlclass/14_Dimensionality_Reduction_files/Image%20[9].png)
            - u는 음수일 수도 있고 양수일 수도 있습니다 별차이 없어요
    - 더 일반적으로 표현하자면
        - nD를 kD로 축소하고자 할 때,
        - 우리는 projection error를 최소화하는 k vector(u<sup>(1)</sup>, ..., u<sup>k</sup>)를 찾아야한다!
- PCA랑 linear regression이랑 무슨 상관이 있을까요?
    - PCA는 linear regression이 아닙니다(외관상 비슷해도 다른거임)
    - linear regression은 각 점과 line사이의 제곱이 **straight line**에 최소화 되도록 합니다
        - NB : 점과의 Vertical distance
    - PCA는 **orthogonal distance**가 최소화되도록 합니다
    - 더 일반화 하자면
        - linear regression : y를 예측
        - PCA : y가 아니라... 우리는 많은 feature가 있고, 모든 feature를 동일하게 다룹니다!!
## PCA Algorithm
- PCA를 하기 전에, data 전처리가 필요합니다
- unlabeled example들이 들어왔을 때 우리는..
    1. Mean normalization
        - x<sub>j</sub><sup>i</sup>를 x<sub>j</sub> - &mu;<sub>j</sub> 로 바꿔줍니다
        - 다르게 말하자면, 각 feature의 mean을 결정하고난 후, 각 feature 값을 평균이랑 뺌으로써 mean을 rescale해줍니다
    2. Feature scaling (depending on data)
        - 만약 feature들이 많이 다른 scale을 갖고있다면, scaling을 해줌으로써 비슷한 정도의 scale을 가질 수 있게 됩니다
        - x<sub>j</sub><sup>i</sup>를 (x<sub>j</sub> - &mu;<sub>j</sub>) / s<sub>j</sub>로 바꿔줍니다
        - s<sub>j</sub>는 range의 정도
- 전처리가 끝나면, PCA는 제곱의 합을 최소화하는 더 낮은 dimensional sub-space를 찾습니다 아래는 2D-1D 예시입니다
    - ![2D-1D](http://www.holehouse.org/mlclass/14_Dimensionality_Reduction_files/Image%20[11].png)
    - 우리는 두가지를 계산해야 됩니다!
        1. u vector
            - 새 평면
        2. z vector
            - 새로운 lower dimensionality feature vectors 입니다
    - u vector를 계산하는 것이 쉽지는 않을텐데 한번 해보면 그리 어렵진 않을거에요
### Algorithm description
- nD -> kD
    - covariance matrix(공분산 행렬)을 계산하자
    - ![covarianceMatrix](http://www.holehouse.org/mlclass/14_Dimensionality_Reduction_files/Image%20[12].png)
        - 위 &Sigma;는 (왼쪽에 작은거) [n x n] matrix입니다
            - x<sup>i</sup>는 [n x 1] matrix인거 기억하기
        - MATLAB에서는 아래처럼 표현
        - ![covariance_matrix_MATLAB](http://www.holehouse.org/mlclass/14_Dimensionality_Reduction_files/Image%20[13].png)
    - &Sigma;의 eigenvector를 계산해보자
        - [U, S, V] = svd(sigma)
            - svd : singular value decompositions
                - eig보다 안정적
            - egi 또한 eigenvvector를 만들어내줄수있다
    - U, S, V는 모두 matrix 입니다
        - U는 [n x n] matrix
        - U의 columns는 u vector로 우리가 원하던 것!!
        - nD - > kD가 목표니까 첫번째 k-vectors만 U vector에서 빼옵니다
        - ![U-vector](http://www.holehouse.org/mlclass/14_Dimensionality_Reduction_files/Image%20[14].png)
- 다음으로 x(n dimensional)을 z(k dimensional)로 바꿔봅시다
    - u matrix에서 첫 k columns만 빼온 후 이것을 세로로(stack) 쌓습니다
        - n x k matrix를 U<sub>reduce</sub>라고 부릅시다
    - 아래처럼 z를 계산해봅시다
        - z = (U<sub>reduce</sub>)<sup>T</sup> * x
            - [k x n]*[n x 1] = [k x 1]
            - 이게 뭔지 글쓴이(외국인 저자)도 알수없음
- 데이터에 label이 없다는거 빼고 지도학습이랑 똑같습니다!
- 요약하자면..
    - 전처리
    - sigma 계산 (covariance matrix)
    - svd로 eigenvectors 계산
    - U에서 k vector 빼오기(U<sub>reduce</sub>=U(:,1:k);)
    - z 계산하기(z = U<sub>reduce</sub>'*x;)
## Reconstruction from Comprssed Representation
- low dimensionality를 다시 higher dimensionality로 복구할 수 있을까요?
- Reconstruction(복원)
    - ![example](http://www.holehouse.org/mlclass/14_Dimensionality_Reduction_files/Image%20[15].png)
    - 우리는 examples(x<sup>1</sup>, x<sup>2</sup> etc)를 갖고있습니다
- Considering
    - z(vector) = (U<sub>reduce</sub>)<sup>T</sup> * x
- 반대로 하는 방법은 아마도...
    - x<sub>approx</sub> = U<sub>reduce</sub> * z
        - U<sub>reduce</sub> = [n x k]
        - z = [k x 1]
        - 따라서 x<sub>approx</sub> = [n x 1]
- 아래처럼 표현될 것입니다
- ![example2](http://www.holehouse.org/mlclass/14_Dimensionality_Reduction_files/Image%20[16].png)
    - 위의 이미지와 달리 정보를 조금 소실하게 됩니다.

## Choosing the number of Principle Components
- 몇 차원(k)으로 줄일지 어떻게 정할까요...
    - k = number of principle components
- 어떻게 PCA가 돌아가는지 생각하고 k를 정해봅시다
    - ![PCAwork](http://www.holehouse.org/mlclass/14_Dimensionality_Reduction_files/Image%20[17].png)
        - PCA는 위에서 설명한 것처럼 projection error를 줄이려합니다
    - ![Total_Variation](http://www.holehouse.org/mlclass/14_Dimensionality_Reduction_files/Image%20[18].png)
        - 데이터의 총 변화량은 본래의 데이터에서 얼마나 떨어져있는지로 나타낼 수 있습니다
- 우리는 k를 아래같은걸 사용해서 정할 수 있습니다
    - ![equation](http://www.holehouse.org/mlclass/14_Dimensionality_Reduction_files/Image%20[19].png)
    - 데이터의 총 변동 대비 projection error의 비율은 위와같이 계산하고, 이것이 작기를 기대합니다(위는 variation(분산)이 99%유지됨을 의미)
    - x<sup>i</sup>랑 x<sub>approx</sub><sup>i</sup>가 비슷할수록 작아집니다
- 이것으로 k를 정합니다
- 종종 variance는 유지한 채로 dimension을 줄일 수 있습니다
- ![algorithm](http://www.holehouse.org/mlclass/14_Dimensionality_Reduction_files/Image%20[20].png)
## Advice for Applying PCA
- PCA를 사용함으로써 실행시간이 단축됩니다
    - 왜그런지 설명할거고
    - 조언을 좀 하겠습니다
### Speeding up supervised learning algorithms
- 만약 100*100 images로 학습을 시킨다고 가정합시다.
- 학습속도는 느릴것이고...
- PCA를 이용하여 dimension을 낮추고 다루기 쉽게 만들어봅시다!
- HOW?
    1. x들을 추출합시다
        - unlabeled training set을 얻었다
    2. x vector에 PCA를 적용합시다
        - vector z로 차원을 축소해봅시다
    3. new training set을 얻었다!
        - 각 vector들은 다시 label과 연결 되었습니다
    4. learning algorithm에 새 tarining set을 넣어봅시다
        - y를 label로 사용하고, z를 feature vector로 사용하자!
    5. 만약 higher dimensionality vector에서 lower dimensionality vector로 새로운 example map을 갖고있다면, learning algorith에 넣어줍시다
- PCA는 어떤 vector를 더 낮은 차원의 vector로 매핑해줍니다
    - x -> z
    - PCA는 **training set에만 사용**하세요!!
    - 이 매핑은 parameter의 set을 계산합니다
        - feature scaling values
        - U<sub>reduce</sub>
            - PCA에 의해 학습된 parameter
    - 이 학습된 parameter들을 아래에 사용할 수 있습니다
        - cross validation data
        - Test set
- algorithm에 큰 피해를 입히지 않고 데이터 차원을 5~10배정도 줄일 수 있습니다.
## Applications of PCA
- Compression
    - 제가 왜 그래야하죠?
        - 데이터를 저장하는데 필요한 메모리랑 디스크 용량을 줄일 수 있음
        - learning algorithm의 속도향상
    - k는 variance를 얼마나 유지하는지 %를 보고 결정합니다
- Visualization
    - 일반적으로 k는 2나 3으로 정합니다
        - 그래야 그릴 수 있습니당...
    - 종종 PCA에 대해 잘못 여겨지는 것...
        1. PCA를 overfitting에 사용함
            - Reasoning
                - x<sup>i</sup>가 n개의 feature를 가지고 있다면, z<sup>i</sup>는 k개의 feature를 가질 것
                - 대충 특징이 적으니까 over fit되지 않을 것이라고 생각하지...
            - This dosen't work!!!!
                - 잘못된 적용이라고!
                - 돌아가긴 하는데 과적합에 맞진 않아
                - 차라리 정규화를 쓰라고
            -PCA는 손실되는 가치를 알지 못하고 일부 데이터를 버립니다.
                - 대부분의 정보를 갖고있으면 괜찮을거야
                - 근데 만약에 중요한걸 버렸다면??
                - 그래서 우리는 95~99%의 variance를 유지해야해
        2. 또다른 이용!
            - 처음부터 PCA로 ML system 설계
            - PCA 없이 system 동작 보기
            - PAC는 언제든 쉽게 추가할 수 있으니까 처음에 할땐 PCA없이 하기