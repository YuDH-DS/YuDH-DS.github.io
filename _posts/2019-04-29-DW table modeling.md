---
title: Data Warehouse modeling
author: Yu Donghwi
date: 2019-04-29
category: Jekyll
layout: post
---

## 1. Data Warehouse ##
 Data Warehouse는 ODS에서 near real time으로 ETL한 data source를 전사 차원에서 공유할 수 있도록 단일한 형식으로 ETL한 DB를 의미한다. DW에 적재된 데이터는 소규모 DW인 Data Mart로 다시 ETL된다.
 
 DW는 대규모 시계열 데이터를 오랫동안 축적하고 있다. 그리고 업무 단위가 아닌 주제 중심으로, 단일 형식으로 데이터를 저장하고 있어 데이터의 활용성과 가용성을 높여준다.

>##### ETL(Extract, Transform, Load)
>
> Interfacing -> Staging -> Profiling -> Cleansing -> Integration -> Export/De-normalization
{: .block-tip }

## 2. Star(Join) schema ##

![](https://github.com/user-attachments/assets/ca8cb7fc-a94f-492c-8894-913fa87beeb5)

 가장 기본적인 형태의 DW table model이다. 모든 attribute를 포함하고 있는 단일의 Fact table을 중심으로 Fact table의 각 column을 설명해주는 다수의 Dimensioanl table들이 join되어 있는 형태이다. 전통적인 DB에서도 다차원DB를 구현할 수 있으며 복잡도가 낮다는 장점이 있다. 그러나 Normalization(정규화)단계가 낮으므로 데이터의 중복이 많아 비효율적이다.


## 3. Functional Dependency and Normalization ##

### 1NF ###

![](https://github.com/user-attachments/assets/de7580e5-9d0d-49af-8bd3-e08abba074ca)

하나의 tuple이 특정 attribute key에 두 개 이상의 value를 할당 받은 경우 '원자성'에 반하며 중복이 발생한다. 따라서 위와 같이 원자성에 위배되는 tuple을 원자화하여 중복을 제거한 것을 1NF(1차 정규화)라고 한다.

### Partial Functional Dependency and 2NF ###

![](https://github.com/user-attachments/assets/845a419b-fbe6-4d33-8e40-c0c29b0e7ee4)

기본키는 모든 속성에 대한 결정자가 되어야 하며, 모든 속성은 기본키에 대한 종속되어야 한다. 그러나 기본키가 복합키인 경우 기본키를 구성하는 일부 속성 만으로도 결정지어지는 속성이 있는 경우가 있다. 위의 relation에서도 ('고객명', '서비스 이름')이 기본키이지만 '서비스 이용 기간'은 복합 키의 도움을 받지 않더라도 '서비스 이름'만으로도 결정지어진다. 이러한 경우를 특정 속성이 기본키의 부분에 종속되었다는 의미로 부분 함수 종속(Partial Functional Dependency)이라고 부르며 이렇게 기본키의 부분에 의해 종속되는 속성을 분리하는 것을 2NF(2차 정규화)라고 한다.


### Transitive Dependency Functional Dependency and 1NF ###

![](https://github.com/user-attachments/assets/5d92ed33-c421-4198-b33f-220c5c678763)

### BCNF ###

![](https://github.com/user-attachments/assets/6aeac377-9b73-4d81-9b6d-46e43ee19934)

### 4NF ###

![](https://github.com/user-attachments/assets/5b6fc97f-9002-463f-8c1a-ed2907f7d212)

### 5NF ###

![](https://github.com/user-attachments/assets/7c3eebae-18b8-4c1b-b75f-255456fc2fc4)


## 4. Snowflake schema ##

![](https://github.com/user-attachments/assets/c281d1c6-d6fe-404d-99b2-41b6443a3814)