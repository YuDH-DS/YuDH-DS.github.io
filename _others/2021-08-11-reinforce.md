---
title: RL(Reinforcement Learning)
author: Yu Donghwi
date: 2021-08-11
category: Jekyll
layout: post
---

# About Reinforcement Learning

 AI의 학습 방식은 크게 지도학습과 비지도학습으로 나뉜다. 지도학습은 AI가 정답이 정해진 훈련용 데이터를 통해 학습한 후 정답이 정해지지 않은 테스트 데이터에 대한 정답을 예측하는 방식이다. 반면 비지도 학습은 AI가 정답이 정해진 훈련용 데이터를 받지 않고 곧바로 테스트 데이터를 받은 후 맨 땅에 헤딩을 하며 최적화 방안을 찾아 나가는 방식이다. 대표적인 비지도 학습 방법으로 군집화(klustering)와 강화 학습(RL)이 있으며 아래에 주어진 예시 문제를 통해 강화 학습 메커니즘을 살펴볼 것이다.

<br>
<br>
![](https://github.com/user-attachments/assets/d5316511-8813-4d15-bd42-21426057e08b)
<br>
<br>


#### $S_{t}$ = 상태

상태란 t시점의 '환경' 속에서 'Agent'가 처해있는 상황을 의미한다. 위 문제에서 (b)에 대한 상태는 각 시점에서 b의 위치를 의미하며 이를 설명하는 상태집합은 아래와 같다.
<br>
$S = [ s \vert 10, 11, 7, 8, 4, 3, 2, 1 ]$

#### $A_{t}$ = 행동

#### $\pi_{t}$ = 정책

#### $V_{t}$ = 가치

#### $\rho$ = 할인율

#### R = 보상함수

#### ER = 기대보상함수


# 1. Model based Reinforcement Learning
## MDP(Markov Decision Process)
## Bellman Equation
## DP(Dynamic Programming)


# 2. Non-Model Reinforcement Learning

## 2-1. Monte Carlo Method

## 2-2. Time Difference learning
### 2-2-1. SARSA
### 2-2-2. Q-learning
### 2-2-3. Actor-Critic