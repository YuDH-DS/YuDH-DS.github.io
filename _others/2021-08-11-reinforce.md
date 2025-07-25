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
![](https://github.com/user-attachments/assets/fe9929ce-cba5-4b2c-852b-e483b94614fb)
<br>
<br>


#### $S_{t}$ = 상태

상태란 t시점의 '환경' 속에서 'Agent'가 처해있는 상황을 의미한다. (b)에서 격자보드라는 환경 속에서 각 시점에 Agent인 로봇의 상태는 각 시점에서의 위치를 의미하며 이를 설명하는 상태집합은 아래와 같다.
<br>
<br>
$S = [ s \vert 10, 11, 7, 8, 4, 3, 3, 2, 1 ]$

#### $A_{t}$ = 행동

행동이란 t시점의 '환경'속에서 'Agent'가 취한 선택지를 의미한다. (b)에서 격자보드라는 환경 속에서 각 시점에 Agent인 로봇의 행동은 각 시점에서의 로봇의 선택을 의미하며 이를 설명하는 행동집합은 아래와 같다.
<br>
<br>
$A = [ a \vert East, North, East, North, West, North, West, West, Null] $

#### $R_{t}$ = 보상

보상이란 t시점의 '환경'속에서 'Agent'가 취한 선택에 대해 환경이 Agent에게 제공하는 반대급부이다. (b)에서 격자보드라는 환경 속에서 각 시점에 환경이 로봇에게 제공한 보상을 설명하는 보상집합은 아래와 같다. 
<br>
<br>
$R = [ r \vert 0, 0, 0, 0, -1, 0, 0, 5, Null ]$
<br>
$ \sum_{t=0}&{8}r_{t} = 4 $

#### $\pi_{t}$ = 정책

정책이란 Agent가 각 상태에서 취해야할 행동에 대한 집합이다. 강화 학습은 랜덤으로 초기 정책을 설정한 후 Agent가 환경과 상호작용하는 과정 속에서 정책을 수정해 나가며 보상의 총합을 극대화하는 정책을 찾는 것을 목표로한다. (b)에서 Agent가 받은 초기 정책 및 행동을 수정하며 최적화한 정책은 아래와 같다.
<br>
<br>
$\pi_{(b)} = [East, North, East, North, West, North, West, West, West, ?, ?, ?, ...] $
<br>
$\pi_{(b')} = [East, North, East, North, West, West, West] $

#### $V_{s, \pi}$ = 상태가치함수

상태가치함수란 현시점 현 상태($S_(t) = s$)에서 Agent가 특정 정책을 따랐을 때 환경으로부터 받게 될 누적 보상의 기대값을 의미한다. 즉, 현시점 현상태가 얼마나 좋은 상황인지를 평가할 수 있는 도구가 된다. 이때 RL은 즉각만족가설에 따라 보상이 한 단계라도 더 먼저 주어질 수록 더 큰 가치를 부여해주는 할인율 $\rho$를 고려하여 상태가치함수를 계산한다.
<br>
<br>
$V_{s, \pi} = E[\sum_{n=t}^{n_{\infty}} (r_{n+1} \cdot \rho^{n}) \vert S_{t} = s]

>##### 할인율($\rho$)의 중요성
> 
> 만약 할인율을 고려하지 않는다면 매우 높은 확률로 최단경로가 아닌 다른 경로가 최적 정책으로 선택될 것이다. 예를 들어 위 문제에서도 RL은 10에서 1로 가는 최단 경로를 버려두고 b'을 최적정책으로 선택해버릴 것이다. 따라서 RL에서 hyper-parameter tunning을 통한 최적의 할인율을 찾아내는 과정은 RL의 성능을 좌우하는 정말 중요한 과정이다. 
{: .block-tip }

#### Q_{s, a, \pi} = 상태행동가치함수

상태행동가치함수란 현시점 현 상태에서 특정 행동을 취한($S_(t) = s, A_{t} = a$) 다음, 그 뒤부터 정책 $\pi$를 따랐을 때 환경으로부터 받게 될 누적 보상의 기대값을 의미한다. 즉, 현 상황에서 해당 행위를 행하는 것이 얼마나 좋은 선택지인지를 평가할 수 있는 도구가 되며 아래와 같이 표현할 수 있다.
<br>
<br>
$Q_{s, \pi} = E[\sum_{n=t}^{n_{\infty}} (r_{n+1} \cdot \rho^{n}) \vert S_{t} = s, A_{t} = a]




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