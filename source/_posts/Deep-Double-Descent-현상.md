---
title: Deep Double Descent 현상
date: 2020/10/19 12:19:00
categories:
- DeepLearning
tags:
- DeepLearning
- OpenAI
---

OpenAI에서 발표한 Deep Double Descent 현상에 대해 알아보도록 하겠습니다.

## Deep Dobule Descent
![image](https://user-images.githubusercontent.com/41286195/96395936-e539c300-1200-11eb-9053-03866e79de95.png)


Deep Double Descent란, 딥러닝 모델의 성능이 하강하는 구간이 **두번** 있다는 현상입니다.  
이러한 현상은, 여러가지 변인들에 의해서 관찰됩니다.

## Model-Wise Double Descent
![image](https://user-images.githubusercontent.com/41286195/96396197-97718a80-1201-11eb-93ae-d1f60a26b167.png)

**모델의 크기**를 키우게 되면, Double Descent현상이 일어납니다.  
위 그림을 보면, ResNet18을 CIFAR10,100 데이터셋에 대해, **모델의 크기**를 키워가며 실험을 진행했고, 모든 경우에서 Double Descent 현상을 볼 수 있었습니다.  
또, 이러한 현상은 **label noise**가 있을시 더 두드러지게 나타난다고 합니다.  

## Epoch-Wise Double Descent
![image](https://user-images.githubusercontent.com/41286195/96396586-837a5880-1202-11eb-9cd3-60b01b43306a.png)

**훈련의 시간**, 즉 Epoch수를 늘리게 되도 이러한 Double Descent 현상이 관찰됩니다.  
더 많은 훈련시간이 **과적합**으로 이끈다는 믿음과는 달리, 일정 임계점을 지나면 모델의 과적합이 되돌려진다는 점에서 매우 흥미로운 현상인것 같습니다.  

![image](https://user-images.githubusercontent.com/41286195/96396764-e0760e80-1202-11eb-9c86-cc235a34fdf1.png)

다만, 이러한 Epoch-Wise Double Descent 현상은 모델의 크기가 어느정도 클때 두드러지게 일어나는것으로 생각됩니다.  

## Sample-Wise Non-Monotonicity
![image](https://user-images.githubusercontent.com/41286195/96397904-8165c900-1205-11eb-8f5d-c9cfe1684933.png)

더 많은 데이터가, 오히려 성능이 나빠지게 하는 구간이 있습니다.  
위 그림에서는 Model Size :50 ~100 정도의 구간에서, 4.5배의 Sample을 사용했음에도 불구하고 더 성능이 나쁜 결과를 보여줍니다.  

## Additional Experiences
### Effect of Data Augmentation
![image](https://user-images.githubusercontent.com/41286195/96398066-e9b4aa80-1205-11eb-8b2c-33200c2f7f04.png)

Data Augmentation 을 사용시, 전체적으로 그래프가 오른쪽으로 이동합니다.  
즉, Double Descent현상이 더 늦게 발생합니다.

### Effect of Optimizer
![image](https://user-images.githubusercontent.com/41286195/96398178-31d3cd00-1206-11eb-86f2-4a0d50ac8e5a.png)

Adam 과 SGD의 비교실험입니다. Adam이 미세하게 좀 더 Double Descent 현상이 두드러집니다.  

### Double Descent in transformer model
![image](https://user-images.githubusercontent.com/41286195/96398259-5d56b780-1206-11eb-8bad-b9f0f181818e.png)

CNN모델이 아닌, Transformer 모델에서도 이러한 Double Descent현상을 관찰 할 수 있습니다.

## References
Nakkiran, Preetum, et al. "Deep double descent: Where bigger models and more data hurt." arXiv preprint arXiv:1912.02292 (2019).  
https://arxiv.org/pdf/1912.02292.pdf

