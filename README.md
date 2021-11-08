# Knowledge_Distillation
## Knowledge_Distillation이란?

지식_증류
Distillation(증류)란 불순물이 섞여있는 혼합물에서 특정 성분을 분리시키는 방법을 말한다.
즉 불필요하게 많은 Parameter가 섞여 있는 model로 부터, generalization 성능을 기존 대비 상향시킬 수 있는 knowledge들을 분리해 내는 방법을 말한다.


## Knowledge_Distillation의 목적

딥러닝 모델들은 보편적으로 Layer를 깊게 쌓아 학습을 하고 Classification 이나 Object detection을 수행한다.
하지만 Layer를 깊게 쌓을 경우 학습에 필요한 GPU와 같은 자원과 긴 시간이 필요하다.

![image](https://user-images.githubusercontent.com/48556414/135951002-34079595-b371-4e23-8e6f-1ab3db2b44a4.png)

예를 들어 핸드폰에서 딥러닝 기술을 활용한 어플리케이션을 만들고 사용하고자할 때,
일반적인 딥러닝 모델을 사용하려면, 클라우드서비스에 접속해 GPU와 같은 자원을 이용해야 하지만
"미리 잘 학습된 Teacher network의 지식을 실제로 사용하고자 하는 Student network에 전달하는 것."과 같은
KD기술을 활용하여 미리 학습된 Teacher network의 지식을 토대로 Student network를 생성하여 
보다 적은 자원으로 비슷한 성능을 사용할 수 있고자 함이다.

## Knowledge Distillation 방법

KD의 형태는 다음과 같다.

![image](https://user-images.githubusercontent.com/48556414/135951442-36aed740-6c61-4b76-8044-cc30aff8eebd.png)

1. Teacher model 을 학습한다.

2. Teacher model로 부터 *soft label을 추출하여 *Knowledge distillation loss로 student model을 학습한다.

### Soft Lable?
![image](https://user-images.githubusercontent.com/48556414/135952044-6f3fa9c8-f9e2-4868-ac57-69b913eeaaef.png)

위와 같이 곰, 고양이, 강아지 3가지 클래스를 구분하는 모델이 있을 때, 
왼쪽과 같이 0 또는 1로 구분하는 것을 Hard Lable, 
오른쪽과 같이 총합이 1인 확률로 구분하는 것을 Soft Label이라 한다.
둘 다 학습의 결과는 고양이를 가르키고 있지만, 

Hard Lable의 경우 개와 고양이, 고양이와 강아지 사이의 공통적인 특징에 대한 정보가 모두 사라지는 반면,

Soft Label의 경우 해당 input data에서 고양이와 곰, 고양이와 강아지가 함께 가지고 있는 특징들에 대한 정보를 가지고 있다.

조금 더 구체적인 예시를 들어보자.

![image](https://user-images.githubusercontent.com/48556414/135952620-02214fc4-62f3-462a-8b18-7bb4dc44952b.png)

왼쪽의 강아지 사진을 input data로 학습을 시도한다면,
hard label의 경우 cow dog cat car (0,1,0,0)의 결과를 도출하고
일반적인 softmax의 결과는 cow dog cat car(10^-2, .9,.1, 10^-9)로 조금 극단적이긴 하지만, cow와 cat, car의 특징을 잡아낸다.

#### Softer Softmax

![image](https://user-images.githubusercontent.com/48556414/135952996-0b492527-f1e4-4f48-919b-0dfeeab08fb2.png)

기존 Softmax function에서 Temperature라는 파라미터 T를 추가하여, 0에 가까워 적절한 정보전달이 불가한 데이터(2번재 줄의 cow, car과 같은 정보)를 
좀 더 soft하게 만들어줘서 학습에 잘 반영될 수 있도록 결과값을 수정해주는 역할을 한다.
T가 2~4 정도일 때 distillation이 효과적으로 적용되었다고 알려져 있으며, T가 1이되면 기존 Softmax function과 동일한 결과를 도출한다.




### Knowledge distillation Loss
위의 Soft label을 통해 Teacher model이 Student model에 넘겨줄 지식을 만들어 냈다면, Knowledge distillation Loss는 해당 지식을 통해 Student model을 학습시킨다.

![image](https://user-images.githubusercontent.com/48556414/135954223-08b57b40-8985-440d-b3d0-199b01827f60.png)

첫 번째 항은 Teature model에서 Soft Label을 계산하고, 해당 Soft Label과 동일한 결과를 도출하도록 Student model을 학습시킨다. 
T는 soft label을 계산할 때 사용한 temparture을 동일하게 사용한다.
두 번째 항은 Student model의 출력값과 hard label 사이의 Crossentropy label을 계산한다.
알파는 두 항 사이의 비율을 조절한다.

### Summary
1. Teacher Network가 input data를 학습
2. Student Network 학습
    - Student network soft prediction + Teacher network soft label 을 활용하여 Distillation loss 구성
    - Student network prediction + Original label -> Classification loss 구성 


## Knowledge Distillation의 종류
### Prediction Logit Distiallaton
### Embedding Distillation
### Weight Initialization

## 앞으로의 계획
1. MNIST dataset을 활용한 KD 적용 구현 _구현完
2. VGG19 -> VGG11 KD 구현
3. Resnet 34 -> resnet 18 KD 구현.
4. 자체적인 KD에 대한 생각.

# Reference
blog 
- https://baeseongsu.github.io/posts/knowledge-distillation/
- https://blog.naver.com/horajjan/222148189575
- https://light-tree.tistory.com/196.
- https://medium.com/neuralmachine/knowledge-distillation-dc241d7c2322
- https://blog.lunit.io/2018/03/22/distilling-the-knowledge-in-a-neural-network-nips-2014-workshop/
