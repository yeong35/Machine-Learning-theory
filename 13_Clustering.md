# Clustering
## Unsupervised learning - introduction
- unlabeled data로 학습시키기
- 데이터의 구조를 확인 후, 데이터의 feature에 따라서 그룹별로 데이터를 나눔
- 유용한 곳
    - Market segmentation : 고객을 다른 시장으로 세분화, 그룹화
    - Social network analysis
    - Organizing computer cluster
    - Astronomical data analysis
## K-means algorithm
- 데이터를 일관된 군집으로 자동 그룹화하는 알고리즘
- K-means는 가장 널리 사용되는 클러스터링 알고리즘
- 알고리즘 개요
    1. 랜덤하게 두 점(두 개로 나눌거면)을 클러스터 중심으로 무작위 할당
    2. 각 example을 보고, 두 점 중 어디에 더 가까운지에 따라 두 점을 중심으로한 군집중 하나에 할당됨
    - ![k-meansClustering](http://www.holehouse.org/mlclass/13_Clustering_files/Image%20[1].png)
    3. 랜덤하게 놓은 두 점을 각각 할당된 데이터들의 평균 포인트로 이동시킴
    4. 더이상 point의 이동이 없을때까지 2, 3 반복
- formal definition
    - input
        - K : 클러스터링 할 개수
        - Training set : { x<sup>1</sup>, x<sup>2</sup>, ..., x<sup>n</sup>}
    - Algorithm
        - K cluster centroids를 { &mu;<sup>1</sup>, &mu;<sup>2</sup>, ..., &mu;<sup>n</sup>}라 하자
        - ![k-meansClustering_algorithm](http://www.holehouse.org/mlclass/13_Clustering_files/Image%20[3].png)
            - for loop 1.
                - 이 loop는 x<sup>i</sup>가 가까운 c<sup>i</sup>에  할당되도록 하도록 값을 가변적으로 계속 setting한다
                - i번째 example을 가장 가까운 centroid에 할당하는 것이다.
            - for loop 2.
                - 각 c<sup>i</sup>에 속한 x와 centroid의 평균을 계산한다.
### 분리되지 않은 cluster의 K-means
- K-means는 종종 잘 정의되지 않은 cluster에도 사용될 수 있다.
    - ex) T-shirt sizing
- ![non-clustering](http://www.holehouse.org/mlclass/13_Clustering_files/Image%20[6].png)
- 실제로 존재하지는 않지만 3개의 cluster로 나눌수는 있다

## K-means optimization objective
- K-means도 최적화를 해야된다!(cost fucntion 존재)
- 왜 해야될까
    - 디버깅에 편리
    - clustering를 더 잘하도록 도와줌
- 알고리즘을 돌리는 동안 아래 두 변수들을 추적하자
    - c<sup>i</sup>는 x<sup>i</sup>가 현재 할당되어 있는 클러스터의 index
    - &mu;<sub>k</sub>는 k cluster의 centroid
    - &mu;<sub>c</sub><sup>i</sup>는 x<sup>i</sup>가 속해있는 cluster의 centroid
- ![J](http://www.holehouse.org/mlclass/13_Clustering_files/Image%20[7].png)
    - 이렇게 최적화할 수 있다
### Random initialization
- ![localMinimum](http://www.holehouse.org/mlclass/13_Clustering_files/Image%20[10].png)
- Global minimum을 찾아가는 것이 목표
- 만약, local minimum인지 아닌지 모르겠다면 random initialization을 여러번 해서 동일한 결과가 많으면 그것이 global optimization일 가능성이 크다
- 일반적으로 50~1000번정도 초기화하여 재실행한다
    - 만약 K가 10개 이상이면, 여러번 초기화할 필요가 비교적 적다.(cluster가 세분화 되기 때문에)
## How do we choose the number of clusters?
- 일반적으로 시각화하여서 수동으로 선택함
- 몇개로 나눠야될지 모호할 때가 있기 때문에 어렵다...
1. Elbow method
- k가 많아질 수록, J가 작아진다(cluster가 세분화되기 때문에 각 군집들이 중심으로부터 더욱 가까워짐)
- ![elbowGraph](http://www.holehouse.org/mlclass/13_Clustering_files/Image%20[12].png)
- K를 늘려도 유의미하게 J가 낮아지지 않는 구간의 K를 선택
- elbow라는 꺾인 라인이 불분명할 수 있음
- 별 도움이 안될 수도 있음
2. Another method
- 목적에 따라 K의 개수 나누기(티셔츠 사이즈 등...)
- ![anotherMethod](http://www.holehouse.org/mlclass/13_Clustering_files/Image%20[13].png)