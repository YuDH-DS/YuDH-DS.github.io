---
title: Gradient descent
author: Yu Donghwi
date: 2021-08-10
category: Jekyll
layout: post
---

### 1. Definition ###
 
 딥러닝의 목표는 검증치와 손실(오차)을 최소화하는 예측치를 보여주는 최적의 모델을 찾는 것이다. 따라서 최소화 메커니즘은 DL 모델 성능을 결정짓는 가장 중요한 요소이며, 경사하강법(Gradient descent)는 그 중 가장 기초적인 메커니즘이다. DL 모델이 경사하강법을 채택할 경우 초기값에서 시작해 점차 경사의 일정 비율만큼을 감소시키며 최소값을 탐색해 나간다. 그 메커니즘은 아래의 수식과 같다.
 
 (a = Learning rate = 라그랑지안 승수)

$$ x_{n} = x_{n-1} - a \cdot \partial f(x_{n-1}) $$


### 2. Importance ### 

 어떠한 형태의 곡률을 가진 다변수 함수에도 적용될 수 있으므로 선형회귀분석의 MSE보다 높은 현실 설명력을 가진다. 또한 0~1 사이에서 학습률(Learning rate)을 조정하여 반비례 관계에 있는 학습 속도와 학습 정확도를 목적에 맞게 제어할 수 있다는 장점이 있다. 

### 3. Example ###

$f(x,y) = (x-7)^2 + (y-3)^2$ 

$starting point = (0,0)$

<br>

$\frac{\partial f(x,y)}{\partial x} = 2(x-7)$

$\frac{\partial f(x,y)}{\partial y} = 2(y-3)$

#### Learning rate = 100 % ####

학습 속도를 높이기 위해 학습률을 1까지 높이게 되면 지나친 과대적합의 문제가 발생하여 모델이 두 점 사이를 무한히 진동하며 최소점 (7,3)에 다다를 수 없음을 확인할 수 있다.

$f(x_{0}, y_{0})=f(0,0)=58$

$f(x_{1}, y_{1})=f(14,6)=58$

$f(x_{2}, y_{2})=f(0,0)=58$

$f(x_{3}, y_{3})=f(14,6)=58$

<br>
![](https://github.com/user-attachments/assets/155d5784-2e1b-4e7c-8653-02a11b7ce565)

<br>
<br>
<br>
<br>

#### Learning rate = 0 % ####

최대한 신중하게 학습 정확도를 높이기 위해 학습률을 0까지 낮추게 되면 지나친 과소적합의 문제가 발생하여 모델이 초기점에 영원히 머무르며 최소점 (7,3)에 다다를 수 없음을 확인할 수 있다.

$f(x_{0}, y_{0})=f(0,0)=58$

$f(x_{1}, y_{1})=f(0,0)=58$

$f(x_{2}, y_{2})=f(0,0)=58$

$f(x_{3}, y_{3})=f(0,0)=58$

<br>
![](https://github.com/user-attachments/assets/5801ab94-3d5d-4a6c-bcca-4d261bd97ec0)

<br>
<br>
<br>
<br>

#### Learning rate = 33.333... % ####

과대적합을 피하기 위해 학습률을 낮추자 과소적합에 직면함을 확인했으므로 최적의 학습률을 찾기 위해 조금씩 학습률을 높이며 hyper-parameter tuning을 진행한다.

$f(x_{0}, y_{0})=f(0,0)=58$

$f(x_{1}, y_{1})=f(\frac{14}{3},2)=7.777...$

$f(x_{2}, y_{2})=f(\frac{49}{9},\frac{8}{3})=2.530...$

$f(x_{3}, y_{3})=f(\frac{161}{27},\frac{25}{9})=1.049...$

<br>
![](https://github.com/user-attachments/assets/d3c17121-403b-47c3-851c-140548acd199)

<br>
<br>
<br>
<br>

#### Learning rate = 50% ####

학습률 33.333%는 수렴 속도가 다소 느려 학습률을 0.5까지 증가시킨 결과 한 번의 학습으로 최소값이 달성되었다. 따라서 초기점 (0,0)에서 최적의 학습률은 0.5임을 알 수 있다.

$f(x_{0}, y_{0})=f(0,0)=58$

$f(x_{1}, y_{1})=f(7,3)=0$

<br>
![](https://github.com/user-attachments/assets/8f5f31c9-b5f1-4cf9-b126-3adcb22056c3)


### 4. Weakness ###

#### 4-1. Local Minimum ####

![](https://github.com/user-attachments/assets/9657102d-9c6b-42d0-a581-26818c2fd4de)

예시로 살펴본 원형 함수는 초기점을 어디로 잡든 큰 문제가 발생하지 않는다. 그러나 극점을 갖는 함수의 경우 문제가 발생한다. 운이 나쁘게도 좋지 않은 초기점을 잡아 극소점에 빠지게 된 경우 경사하강법은 이를 최소점으로 인식하여 헤어나오지 못하는 문제가 발생한다.

#### 4-2. Saddle Point ####

![](https://github.com/user-attachments/assets/c2e0acae-f579-4833-8dfb-3075789ed0bf)

평면이 아닌 공간의 경우 평면에 접하는 안장점에 도달할 경우 경사가 0이 되어 경사하강법은 안장점에서 벗어나지 못하게 된다.



### 5. Alternative ###

#### 5-1. Momentum Gradient descent ####

이전 단계에서 감소하며 발생한 관성의 일정 비율을 학습률에 반영시켜 줄 경우 극소점이나 안장점에 도달하더라도 빠져나올 수 있게 되며 메커니즘은 아래와 같다. 이때 관성은 0.9 ~ 1 사이의 관성계수를 통해 지나친 가속을 방지한다.

(m = momentum, b = momentum rate)

<br>

$$ x_{n} = x_{n-1} - m_{n} $$

$$ m_{n} = b \cdot m_{n-1} + a \cdot \partial f(x_{n-1}) $$


#### 5-2. Adaptive Gradient descent ####

초기점을 잘못 잡은 경우 일부 변수는 과대적합되고 일부 변수는 과소적합 되는 불균형의 문제가 발생한다. 이를 방지하기 위해 누적된 경사 하강치만큼 학습률을 줄여주면 변수 간 학습 격차를 줄일 수 있다. 

<br>

$$ c = \Sigma a \cdot f(x) $$

$$ x_{n} = x_{n-1} - \frac{a}{\sqrt{c} + \epsilon} \cdot f(x_{n-1}) $$


#### 5-3. Adam ####

Momentum Gradient descent는 극소점이나 안장점으로 부터 벗어날 수 있어 '방향' 상에서 이점을 가지고 있으나 누적된 관성이 '속력'을 지나치게 가속시킬 수 있다는 단점을 가지고 있다. 반면 Adaptive Gradient는 학습률을 떨어뜨리며 step-by-step 조금더 꼼꼼히 학습한다는 장점이 있다. 따라서 두 메커니즘을 혼합하여 '속도'를 통제하고자 고안된 메커니즘이 바로 Adam이며 구체적인 메커니즘은 아래와 같다.

$m_{n}$ = 방향에 대한 momentum

$v_{n}$ = 속력에 대한 momentum

$b_{m}$ = 방향 관성 계수

$b_{v}$ = 속력 관성 계수

a = 학습률


$$m_{n} = b_{m} \cdot m_{n-1} + (1-b_{m})\cdot \partial f_{n}$$

$$v_{n} = b_{v} \cdot v_{n-1} + (1-b_{v})\cdot (\partial f_{n})^2$$


$$\hat{m_{n}} = \frac{m_{n}}{1-b_{m}}$$

$$\hat{v_{n}} = \frac{v_{n}}{1-b_{v}}$$


$$x_{n} = x_{n-1} - a \cdot \frac{\hat{m_{n}}}{\sqrt{\hat{v_{n}}}+\epsilon}$$

<br>
<br>

> ##### ETC
>
> 이 외에도 Sample을 여러 단위로 쪼개어 gradient를 도출한 후 각 batch의 발생확률에 근거한 경사의 평균을 구하여 다음 단계로 나아가는 SGD, 각 batch의 제곱 평균을 활용하는 RMSProp 등 다양한 gradient descent 메커니즘이 존재한다. 그러나 그 어떠한 메커니즘도 완벽하지 않기 때문에 DA와 DS는 현재의 상황에 맞는 메커니즘을 적절히 선택하는 것이 중요하다.
{: .block-tip }



<br>
<br>
<br>