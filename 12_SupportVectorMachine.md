# 12. Support Vector Machines (SVMs)

- 회귀, 분류, 이상치 탐지 등에 사용되는 지도학습 방식
- 클래스 사이의 경계에 위치한 데이터 포인트를 서포트 벡터(support vector)라고 함
- 각 서포트 벡터가 클래스 사이의 결정 경계를 구분하는데 얼마나 중요한지를 학습
- 각 서포트 벡터 사이의 마진이 가장 큰 방향으로 학습
- 서포트 벡터 까지의 거리와 지서포트지 벡터의 중요도를 기반으로 예측을 수행
- --
- sigmoid function의 cost가 아래와 같다고하자.
    - ![sigmoidFunction](http://www.holehouse.org/mlclass/12_Support_Vector_Machines_files/Image%20[4].png)
- 이때, y=1일 때 costfunction의 그래프는...
    - ![y=1,sigmoidCostFunction](http://www.holehouse.org/mlclass/12_Support_Vector_Machines_files/Image%20[5].png)
- 이때, y=0일 때 costfunction의 그래프는...
    - ![y=0,sigmoidCostFunction](http://www.holehouse.org/mlclass/12_Support_Vector_Machines_files/Image%20[6].png)
### SVM cost functions from logistic regression cost function
- y=1일 때, 자홍색 선으로 cost function 표시
    - ![y=1,SVM](http://www.holehouse.org/mlclass/12_Support_Vector_Machines_files/Image%20[7].png)
- y=1일 때, 자홍색 선으로 cost function 표시
    - ![y=0,SVM](http://www.holehouse.org/mlclass/12_Support_Vector_Machines_files/Image%20[8].png)
### complete SVM cost function
- SVM cost function 식
    - ![SVMcostFunction](http://www.holehouse.org/mlclass/12_Support_Vector_Machines_files/Image%20[10].png)
    
### SVM notation는 조금 달라!
1. 1/m을 지움
    - 1/m을 지워도 같은 optimal value를 얻어야 됨
    - 1/m은 상수니까, 똑같은 optimiztion을 가짐!
        - 1 2 3 4 에 다 5곱해도 맨 앞이 가장 작은건 똑같음
2. CA+B
    - logistic regression에서는 a+&lambda;b형식으로 표시했지만 SVM은 아님
    - 우리는 C라고 불리는 다른 parameter를 사용하여 표기할거야
    - CA+B 이런 식으로
    - 만약 C가 1/&lambda;와 같으면 CA+B랑 a+&lambda;b랑 같은 값을 줄거양
    - ![finalEquation](http://www.holehouse.org/mlclass/12_Support_Vector_Machines_files/Image%20[11].png)
- logistic과 달리 h<sub>&theta;</sub>는 확률을 안줘... 하지만 1또는 0이라는 예측을 바로 얻을 수 있지!
    - 만약 &Theta;<sup>T</sup>x가 0보다 크면~ h<sub>&theta;</sub>는 1, 아니면 0

## Large margin intuition
- SVM은 large margin classifiers라고도 불린다
- 아래는 SVM의 cost fuction이다.
    - ![SVMcostFucntion](http://www.holehouse.org/mlclass/12_Support_Vector_Machines_files/Image%20[12].png)
    - 왼쪽이 cost<sub>1</sub>, 오른쪽이 cost<sub>0</sub>
    - y=1일때, z(&Theta;<sup>T</sup>x)가 1보다 크면, cost는 0
    - y=0일때, z기 -1보다 작으면, cost는 0
- SVM의 흥미로운 특징
    - 만약 내가 positive 예를 갖고 있다면, z가 0보다 크기만 하면 된다. 그렇다면 모델은 1을 예상할 것이다.
    - SVM은 0보다 더 큰 -를 원합니다!
- what are the consequences of this?
    - 만약에, C가 100000이라 엄청 크다고 가정한다면..
    - 우리가 CA+B를 최소화 한다고 가정합시다
    - 그러면 A를 0에 가깝게 골라야겠지?
    - 어떻게 A를 0에 가깝게 만드는지가 이 최적화의 문제임
    - Make A = 0
        - if y=1
            - 위 그래프를 봤을 때, z값이 1보다 크거나 같아야함
        - if y=0
            - 위 그래프를 봤을 때, z값이 -1보다 작거나 같아야함
        - 자 이 모든게 끝나면 B를 작아지는 쪽으로 생각해봅시다! (A가 0되면 A*C는 0이니까 이제 B를 줄여야겠죠?)
    - Make B = 0
        - 아래와 같은 제약을 가지고 B(아래의 첫번째 식)을 최소화 해봅시다
        - ![constraint](http://www.holehouse.org/mlclass/12_Support_Vector_Machines_files/Image%20[13].png)
    - 위를 사용해서 식을 최소화하면 놀라운 결과를 볼 수 있음!
        - 자홍색과 초록색은 logistic regression을 이용해서 decision boundary를 만든 것이고, 검은 색은 SVM이 만든 것
            - ![decision_boundary](http://www.holehouse.org/mlclass/12_Support_Vector_Machines_files/Image%20[14].png)
        - 확실히 logistic regression과는 달리 margin이 큰 쪽으로 분류가 되었습니다
    - C가 엄~청 클 때도 봅시다!
        - ![veryBigC!](http://www.holehouse.org/mlclass/12_Support_Vector_Machines_files/Image%20[17].png)
        - C가 정말정말 크면 자홍색처럼 됩니다. 우리는 이런 방법(SVM)을 사용하여 margin을 극대화 합니다
        - 그래서 이런 SVM은 outlier가 없다면 유용하게 사용될 수 있습니다!(그러니까 몇개의 이상치는 무시할수있단거죠)
## Large margin classification mathematics (optional)
- vector 내적
    - ||u|| = sqrt(a<sup>2</sup>+b<sup>2</sup>) (대충 거리, 길이란 뜻)
    - ![innerProduct](http://www.holehouse.org/mlclass/12_Support_Vector_Machines_files/Image%20[20].png)
    - u<sup>T</sup>v = p*||u||
    - = p*||u|| = u<sub>1</sub>v<sub>1</sub>+u<sub>2</sub>v<sub>2</sub>
- SVM의 decision boundary
    - ![ToDo_is_making_minimum_b](http://www.holehouse.org/mlclass/12_Support_Vector_Machines_files/Image%20[22].png)
    - &Theta;<sub>0</sub>=0, n=2라고 가정하자.(feature가 두개란거지)
    - 위 식대로 정리하면
        - ![euclidDistance](http://www.holehouse.org/mlclass/12_Support_Vector_Machines_files/Image%20[25].png)
        - ![euclidDistance2](http://www.holehouse.org/mlclass/12_Support_Vector_Machines_files/Image%20[26].png)
        - 따라서 SVM은 squared norm을 최소화 한다는 것을 알 수 있습니다
- 그렇다면 (&Theta;<sup>x</sup>x) parameter는 무엇을 할까용?
    - ![ThetaXInnerproduct](http://www.holehouse.org/mlclass/12_Support_Vector_Machines_files/Image%20[30].png)
    - &Theta;와 x의 내적이었답니다
    - p(사실은 p<sup>i</sup>)는 example i의 길이였답니다
    - 위에서 나타낸 조건들을 아래와 같이 나타낼 수도 있게되었습니다~
        - ![ToDo_is_making_minimum_B](http://www.holehouse.org/mlclass/12_Support_Vector_Machines_files/Image%20[31].png)
- 밑의 예제들로 이 함수들을 다시 정의해봅시다
    - 아래와같이 o, x 예제들이 있다고할 때, 우리는 위에서 &Theta;<sub>0</sub>를 0으로 가정했으니 아래와 같이 나타납니다
        - ![SVMdecisionBoundary](http://www.holehouse.org/mlclass/12_Support_Vector_Machines_files/Image%20[33].png)
    - 그런데 이건 너무 예제들과 가까워요
    - ![example1](http://www.holehouse.org/mlclass/12_Support_Vector_Machines_files/Image%20[36].png)
        - &Theta;를 decision boundary에 90도로 그린 후, x<sup>1</sup>을 &Theta;에 직교로 내리고, x<sup>2</sup>도 직교로 내립니다
        - 그러면 p<sup>1</sup>은 양수 p<sup>2</sup>는 음수인것을 볼 수 있습니다.
        - p<sup>1</sup>*||&Theta;||는 -1보다 작거나 같아야하고, p<sup>2</sup>*||&Theta;||는 1보다 크거나 같아야합니다.
        - 이런 문제가 생기는 이유는.. 
            - 우리는 &Theta;의 norm를 최대한 작게 하는게 목표입니다.(위에서 1/2||&Theta;||를 작게 해야 B가 작아진다고 했음)
            - &Theta;가 좋은 방향은 아닌거같아요(p값이 작아짐에 따라서 ||&Theta;||가 커져야하니까!)
            - 따라서 p값을 더 크게 허용하도록 해봅시다(margin을 키우자는 얘기)
        - ![example2](http://www.holehouse.org/mlclass/12_Support_Vector_Machines_files/Image%20[39].png)
            - 새로 decision boundary를 선택하고 &Theta;를 그려봅시다
            - 전보다 훨씬 margin(p)가 커졌습니다!
## Kernels - 1: Adapting SVM to non-linear classifiers
- ![non-linear_classification](http://www.holehouse.org/mlclass/12_Support_Vector_Machines_files/Image%20[40].png)
- 위와 같은 복잡한 polynomial feature를 가진 set이 있다고 가정하자
    - h<sub>&Theta;</sub>(x)는 vector들의 weighted sum이 0보다 작거나 같으면 1, 0보다 크면 0을 return한다고 하자
- 위 가설은, 다양한 고차항 x를 초함하는 새로운 vector f를 곱한 매개 변수 벡터의 합을 더하여 결정 경계를 계산합니다
    - h<sub>&Theta;</sub>(x)=&Theta;<sub>0</sub>+&Theta;<sub>1</sub>f<sub>1</sub>+&Theta;<sub>2</sub>f<sub>2</sub>+&Theta;<sub>3</sub>f<sub>3</sub>
        - f<sub>1</sub> = x<sub>1</sub>
        - f<sub>2</sub> = x<sub>1</sub>x<sub>2</sub>
        - f<sub>3</sub> = x<sub>1</sub>x<sub>2</sub>x<sub>3</sub>
- ![newFeatures](http://www.holehouse.org/mlclass/12_Support_Vector_Machines_files/Image%20[41].png)
    - l<sup>1</sup>~l<sup>3</sup>가 있을때 이것들을 landmarks라고 부르자!
    - x가 주어졌을 때, f1은 (x, l<sup>1</sup>)사이의 유사성으로 정의된다
    - f들의 정의는 아래와 같다
    - ![Define_f](http://www.holehouse.org/mlclass/12_Support_Vector_Machines_files/Image%20[42].png)
    - 위와같은 similarity function을 **kernel**이라 한다
        - 그리고 이 함수는 **Gaussian Kernel**이다
    - 이제부터 f1=k(x, l<sup>1</sup>)라고 표기한다
### Diving deeper into the kernel
- 커널이 왜 유의미한지 알아보자
    - x가 landmark랑 엄청 가까이 있으면 spared distance가 0과 가까워진다
    - ![f_1=exp](http://www.holehouse.org/mlclass/12_Support_Vector_Machines_files/Image%20[44].png)
    -  따라서 f<sub>1</sub>는 1과 가까워진다
    - 만약 x랑 landmark랑 아주 멀다면, f_1는 0에 가까워진다
    - 이 landmark들은 new feature로 정의된다
    - ![3D](http://www.holehouse.org/mlclass/12_Support_Vector_Machines_files/Image%20[45].png)
- &sigma;(표준편차)는 무엇을 하는가?
    - &sigma;<sup>2</sup>(분산)은 gaussian kernel의 매개변수고, landmark 주변 상승의 가파른 정도를 정의
    - &sigma;<sup>2</sup>가 1일때
        - ![sigma^2=1](http://www.holehouse.org/mlclass/12_Support_Vector_Machines_files/Image%20[46].png)
    - &sigma;<sup>2</sup>가 3일때
        - ![sigma^2=3](http://www.holehouse.org/mlclass/12_Support_Vector_Machines_files/Image%20[47].png)
    - &sigma;<sup>2</sup>가 클수록 f1이 천천히 떨어짐을 볼 수 있다.
- training example x에서 아래와 같으면 1이라고 예상한다
- h<sub>&Theta;</sub>(x)=&Theta;<sub>0</sub>+&Theta;<sub>1</sub>f<sub>1</sub>+&Theta;<sub>2</sub>f<sub>2</sub>+&Theta;<sub>3</sub>f<sub>3</sub>
- &Theta;<sub>0</sub>+&Theta;<sub>1</sub>f<sub>1</sub>+&Theta;<sub>2</sub>f<sub>2</sub>+&Theta;<sub>3</sub>f<sub>3</sub> >= 0
    - &Theta;<sub>0</sub> = -0.5
    - &Theta;<sub>1</sub> = 1
    - &Theta;<sub>2</sub> = 1
    - &Theta;<sub>3</sub> = 0
- ![example1](http://www.holehouse.org/mlclass/12_Support_Vector_Machines_files/Image%20[48].png)
    - 이때 x가 분홍점이라면, l^1는 1 나머지는 0에 가까울 것. 위에서 본 공식을 적용하면 0.5니까 1을 예측
- ![example2](http://www.holehouse.org/mlclass/12_Support_Vector_Machines_files/Image%20[49].png)
    - 이때 x가 하늘색 점이라면, -0.5니까 0으로 예측
- 우리는 l<sup>1</sup>, l<sup>2</sup>에 가까워야 1이라 에측하고 l<sup>3</sup>과 가까우면 0을 예측한다
    - ![decisionBoudary](http://www.holehouse.org/mlclass/12_Support_Vector_Machines_files/Image%20[50].png)

## Kernels II
- landmark를 선택하는 방법에 대해 얘기하고, kernel을 정의하고, hypothesis function을 만들어보자
1. choosing the landmarks
- 각 training set과 정확히 같은 자리에 landmark를 표시한다
    - 특징들의 평균(means)은 training set과 얼마나 가까운지 측정합니다
- 새로운 example이 주어진다면, 모든 f 값을 계산한다
    - f(f<sub>0</sub>, ..., f<sub>m</sub>)
        - f<sub>0</sub> = 1
        - f<sub>1</sub><sup>i</sup> = k(x<sup>i</sup>, l<sup>1</sup>)
        - f<sub>2</sub><sup>i</sup> = k(x<sup>i</sup>, l<sup>2</sup>)
        - ...
        - f<sub>m</sub><sup>i</sup> = k(x<sup>i</sup>, l<sup>m</sup>)
    - f들 사이에서 자신의 f와 x를 비교한다(f<sub>i</sub><sup>i</sup>랑!)
        - 우리가 Gaussian kernel을 사용하니까 이 값은 1일 것이다(x와 landmark가 가까울수록 1에 가깝다고 함)
### SVM hypothesis prediction with kernels
- y = 1, if(&Theta;<sup>T</sup>f >= 0)
    - &Theta; = [m+1 x 1]
    - f = [m+1 x 1]
    - &Theta;만 있으면 y를 예측할 수 있다! 근데 &Theta;는 어떻게 예측하지?
### SVM training with kernels
- ![SVM_CostFunction](http://www.holehouse.org/mlclass/12_Support_Vector_Machines_files/Image%20[51].png)
    - f를 사용하여(x를 사용하는 대신) cost function을 줄일 수 있다
    - 그러면서 SVM에 대한 parameter를 구할 수 있다
- m = n이라고 하자
    - 왜냐면 feature의 수는 우리가 갖고있는 training set의 수와 같음(위에 training set에 같은자리에 landmark를 놓음)
- 이때 B부분을 보면..
    - ![B_part](http://www.holehouse.org/mlclass/12_Support_Vector_Machines_files/Image%20[52].png)
        - &Theta;<sub>0</sub>를 제외하면 위와 같다
- 많은 구현에서 아래를 수행합니다
    - ![ㅇㅂㅇ](http://www.holehouse.org/mlclass/12_Support_Vector_Machines_files/Image%20[52].png)
        - 내가 만든 커널이 matrix M에 의존한다면
            - 최소화 하는 방법이 조금 다를 것(&Theta;을 재정의 한다는 뜻)
            - 더 효율적이고 큰 training set에 적용할 수 있다
            - 만약에 training set이 10000개라면, feature가 10000개라는 것
                - 다 for문으로 계산하지않고 matrix multiplication algorithm을 사용함!
    - 이 kernel을 다른 알고리즘에도 적용할 수 있겠지만..
        - 계산 비용이 크고 SVM이 훨씬 효율적이야!
- SVM parameter중 C에 대하여...
    - bias and varience를 조정합니다
    - C는 1/&lambda;와 유사한 역할을 함
    - C가 크면 low bias, high variance (overfitting)
    - C가 작으면 high bias, low variance (underfitting)
- SVM parameter중 &sigma;<sup>2</sup>에 대하여...
    - &sigma;<sup>2</sup>가 크면... f feature들이 부드러운 모양(high bias, low variance)
    - &sigma;<sup>2</sup>가 작으면... f feature들이 가파른 모양(low bias, high variance)
## SVM - implementation and use
- 지금까지 Gaussian kernel에 대해 알아봤다
    - &sigma;에 대한 정의가 필요함
- 언제 Gaussian을 사용할 수 있을까?
    - n이 작거나 또는 m이 큰 경우에 사용할 수 있음(2D training set은 큰거야)
    - 만약 gaussian kernel을 사용한다면 kernel function이 필요할 것임
- NB : Gaussian kernel을 사용하기 전에 **feature scaling**을 해야함
    - 안그러면 큰 값들이 f value들을 지배하게됨
- linear kernel (커널 사용x)
    - (&Theta;<sup>T</sup>x) >= 0인경우, y = 1을 예측
        - 그래서 f value가 없음
    - 만약 n이 크고, m이 작으면...
        - feature는 많고... example은 별로 없으니 overfitting이 나타날 수 있다
- Other choice of kernel
    - Linear, Gaussian이 제일 흔함
    - 모든 similarity function들이 유효한 kernel은 아님
    - Polynomial kernel
        - (x<sup>T</sup>l+Con)<sup>D</sup>
        - 비슷할수있어도 inner product 값은 클 수 있다
        - two parameters
            - Degree of polynomial (D)
            - Number you add to l (Con)
        - Gaussian kernel보다 성능이 별로일거임
    - String Kernel
        - input이 text string일때 사용
        - text classification에 사용
    - ...
### Multi-class classification for SVM
- 많은 package들이 multi-class classification package를 갖고있음
- 근데 없으면 one-vs all method 사용하면됨
- 크게 중요하진 않아용

### Logistic regression vs. SVM
1. n(feature)가 큰 경우 m(training set)
    - ex) feature vector dimension = 10000, traing set : 10 ~ 1000
    - linear kernel과 함께 logistic regression또는 SVM 사용
2. n이 작고 m이 중간정도면
    - ex) n = 1~1000, m = 10 ~ 10000
    - Gaussian kernel
3. n이 작고, m이 크면
    - ex) n = 1~1000, m = 50000 ~
    - feature를 더 늘리고 linear kernel과 함께 SMV의 logistic regression 사용하기
- SVM은 복잡한 non-linear함수를 학습하기위해 다른 kernel을 사용
- 그러나 neural network가 잘 설계되어야함(그렇지 않다면 SVM이 좀 느릴거임)