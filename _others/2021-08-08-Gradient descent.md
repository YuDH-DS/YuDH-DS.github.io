---
title: Gradient descent
author: Yu Donghwi
date: 2021-08-10
category: Jekyll
layout: post
---

### 1. Definition ###
 
 딥러닝의 목표는 검증치와 손실(오차)을 최소화하는 예측치를 보여주는 최적의 모델을 찾는 것이다. 따라서 최소화 메커니즘은 DL 모델 성능을 결정짓는 가장 중요한 요소이며, 경사하강법(Gradient descent)는 그 중 가장 기초적인 메커니즘이다. DL 모델이 경사하강법을 채택할 경우 초기값에서 시작해 점차 경사를 감소시켜나가며 최소값을 탐색해 나가며, 이는 아래의 수식과 같다.(a=Learning rate)

$$ x_{n} = x_{n-1} - a \cdot \partial f(x_{n-1}) $$


### 2. Importance ### 

 어떠한 형태의 곡률을 가진 다차원 함수에도 적용될 수 있으므로 선형회귀분석의 MSE보다 높은 현실 설명력을 가진다. 또한 0~1 사이에서 학습률(Learning rate)을 조정하여 반비례 관계에 있는 학습 속도와 학습 정확도를 목적에 맞게 제어할 수 있다는 장점이 있다. 

### 3. Example ###

$f(x,y) = (x-7)^2 + (y-3)^2$ 

<br>

$\frac{\partial f(x,y)}{\partial x} = 2(x-7)$

$\frac{\partial f(x,y)}{\partial y} = 2(y-3)$

<br> when, starting point = (0,0), Learning rate = 100 %
학습 속도를 높이기 위해 학습률을 100%까지 높이게 되면 지나친 과대적합의 문제가 발생하여 모델이 두 점 사이를 무한히 진동하며 최소점 (7,3)에 다다를 수 없음을 확인할 수 있다.

$f(x_{0}, y_{0})=f(0,0)=58$

$f(x_{1}, y_{1})=f(14,6)=58$

$f(x_{2}, y_{2})=f(0,0)=58$

$f(x_{3}, y_{3})=f(14,6)=58$

![](https://github.com/user-attachments/assets/155d5784-2e1b-4e7c-8653-02a11b7ce565)

<br>
<br>
<br> when, starting point = (0,0), Learning rate = 100 %
최대한 신중하게 학습 정확도를 높이기 위해 학습률을 0%까지 낮추게 되면 지나친 과소적합의 문제가 발생하여 모델이 초기점에 영원히 머무르며 최소점 (7,3)에 다다를 수 없음을 확인할 수 있다.

$f(x_{0}, y_{0})=f(0,0)=58$

$f(x_{1}, y_{1})=f(0,0)=58$

$f(x_{2}, y_{2})=f(0,0)=58$

$f(x_{3}, y_{3})=f(0,0)=58$

![](https://github.com/user-attachments/assets/5801ab94-3d5d-4a6c-bcca-4d261bd97ec0)



### 4. Weakness ###


### 5. Alternative ###