# Neural Networks: Representation

## Model Representation 1
- x<sub>0</sub> : bias unit, 언제나 1이다.
- logistic function을 classification이라고도 하고 activation function이라고도 한다.
- theta를 weight라고 부르기도 한다.
- 첫 layer를 input layer, 마지막 layer를 output layer, 가운데 layer들을 hidden layer라고 한다.
- 이러한 중간 layer의 노드들을 a<sub>0</sub><sup>2</sup>...a<sub>n</sub><sup>2</sup> activation unit이라고 부른다.
    - a<sub>i</sub><sup>(j)</sup> : j layer의 i번째 unit
    - &Theta;<sup>(j)</sup> : j layer에서 j+1 layer로 매핑해주는 weight 행렬
        - s<sub>j</sub> : j layer의 unit들
        - &Theta;<sup>j</sup>의 dimensions : [s<sub>j+1</sub>*s<sub>j</sub>**+1**]
            - +1은 bias nodes입니당
            
## Model Representation 2
- forward propagation
    - forward propagation은 각 layer를 연속적으로 계산하여 다음 layer로 전달함
    - z<sub>k</sub><sup>(j)</sup>=&Theta;<sub>k,0</sub><sup>(j-1)</sup>x<sub>0</sub>+&Theta;<sub>k,1</sub><sup>(j-1)</sup>x<sub>1</sub>+...+&Theta;<sub>k,n</sub><sup>(j-1)</sup>x<sub>n</sub>
    - a<sub>j</sub><sup>(i)</sup>=g(z<sub>j</sub><sup>(i)</sup>)
    - z<sup>(j)</sup>=&Theta;<sup>(j-1)</sup>a<sup>(j-1)</sup>