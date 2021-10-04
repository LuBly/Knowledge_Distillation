# Knowledge_Distillation
## Knowledge_Distillation이란?

지식_증류
Distillation(증류)란 불순물이 섞여있는 혼합물에서 특정 성분을 분리시키는 방법을 말한다.
즉 불필요하게 많은 Parameter가 섞여 있는 model로 부터, generalization 성능을 기존 대비 상향시킬 수 있는 knowledge들을 분리해 내는 방법을 말한다.


## Knowledge_Distillation의 목적

딥러닝 모델들은 보편적으로 Layer를 깊게 쌓아 학습을 하고 Classification 이나 Object detection을 수행한다.
하지만 Layer를 깊게 쌓을 경우 학습에 필요한 GPU와 같은 자원과 긴 시간이 필요하다.

예를 들어 핸드폰에서 딥러닝 기술을 활용한 어플리케이션을 만들고 사용하고자할 때,
일반적인 딥러닝 모델을 사용하려면, 클라우드서비스에 접속해 GPU와 같은 자원을 이용해야 하지만
"미리 잘 학습된 Teacher network의 지식을 실제로 사용하고자 하는 Student network에 전달하는 것."과 같은
KD기술을 활용하여 미리 학습된 Teacher network의 지식을 토대로 Student network를 생성하여 
보다 적은 자원으로 비슷한 성능을 사용할 수 있고자 함이다.

## Knowledge Distillation 방법
### Prediction Logit Distiallaton
### Embedding Distillation
### Weight Initialization
1. Soft Label
2. distillation Loss


# Reference
blog 
- https://baeseongsu.github.io/posts/knowledge-distillation/
- https://blog.naver.com/horajjan/222148189575
- https://light-tree.tistory.com/196
