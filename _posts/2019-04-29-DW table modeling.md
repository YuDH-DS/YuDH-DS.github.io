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

### 1NF and Atomicity ###

![](https://github.com/user-attachments/assets/de7580e5-9d0d-49af-8bd3-e08abba074ca)

하나의 tuple이 특정 attribute key에 두 개 이상의 value를 할당 받은 경우 '원자성'에 반하며 중복이 발생한다. 따라서 위와 같이 원자성에 위배되는 tuple을 원자화하여 중복을 제거한 것을 1NF(First Normal Form)라고 한다.

### 2NF and Partial Functional Dependency ###

![](https://github.com/user-attachments/assets/845a419b-fbe6-4d33-8e40-c0c29b0e7ee4)

기본키는 모든 속성에 대한 결정자가 되어야 하며, 모든 속성은 기본키에 대한 종속되어야 한다. 그러나 기본키가 복합키인 경우 기본키를 구성하는 일부 속성 만으로도 결정지어지는 속성이 있는 경우가 있다. 위의 relation에서도 ('고객명', '서비스 이름')이 기본키이지만 '서비스 이용 기간'은 복합 키의 도움을 받지 않더라도 '서비스 이름'만으로도 결정지어진다. 이러한 경우를 특정 속성이 기본키의 부분에 종속되었다는 의미로 부분 함수 종속(Partial Functional Dependency)이라고 부르며 이렇게 기본키의 부분에 의해 종속되는 속성을 분리한 것을 2NF(Second Nomal Form)라고 한다.


### 3NF and Transitive Functional Dependency ###

![](https://github.com/user-attachments/assets/5d92ed33-c421-4198-b33f-220c5c678763)

이행 함수 종속(Transitive Functional Dependency)이란 기본키 X에 종속되는 속성 Y가 속성 Z를 결정하여 X가 Z를 결정하게 되는 것을 의미한다. 이때 Z는 relation내에서 무의미하기 때문에 Y,Z를 분리하게 될 경우 중복을 줄일 수 있다. 위의 table에서도 기본키인 '책번호'가 '출판사'를 결정하고, '출판사'가 다시 '홈페이지'를 결정하는 이행 함수 종속이 발생하였다. 따라서 '홈페이지'를 분리할 경우 중복을 줄일 수 있으며 이를 3NF(Thrid Normal Form)라고 한다.  



### BCNF and Determinant Functional Dependency ###

![](https://github.com/user-attachments/assets/6aeac377-9b73-4d81-9b6d-46e43ee19934)

결정자 함수 종속성이란 기본키가 복합키일 경우 기본키를 구성하는 일부 속성이 기본키가 아닌 다른 속성에 의해 종속되는 현상을 의미한다. 위의 table의 경우 ('학번', '과목명')이 기본키로서 '교수명'을 결정짓지만 종속자인 '교수명'이 prime key의 일부인 '과목명'의 결정자가 되어 결정자 함수 종속성이 발생하였다. 이러한 경우 prime key에 결정력을 행사하는 속성을 분리할 경우 중복을 제거할 수 있으며 이를 BCNF(Boyce codd Normal Form)라고 한다. 


### 4NF and Multi value Dependency ###

![](https://github.com/user-attachments/assets/5b6fc97f-9002-463f-8c1a-ed2907f7d212)

위 entity에서 '개발자' key는 '자격증' 속성과 '언어' 속성이라는 다수의 속성을 종속하는데 종속자들 간에는 서로 독립적이다. 이러한 관계를 다치 종속성(Multi value dependency)이라고 한다. 이때 각각의 종속자 별로 table을 나눠주면 중복을 제거하고 더욱 효율적인 DB를 설계하는 것을 4NF(Fourth Normal Form)이라고 한다.


### 5NF and Join Dependency ###

![](https://github.com/user-attachments/assets/7c3eebae-18b8-4c1b-b75f-255456fc2fc4)

앞서 제시한 4NF entity를 다시 '개발자' 테이블을 기준으로 JOIN하게 되면 Cartesian product가 수행되며 (홍길동, 정보처리기사, C++), (홍길동 빅데이터분석기사 C)라고 하는 tuple이 형성되며 무결성이 침해된다. 이처럼 4NF를 다시 JOIN할 때 무결성이 침해되는 것을 Join Dependency라고 부르며 이를 해결하기 위해 모든 속성들이 가진 종속관계 별로 relation을 분리한 것을 5NF(Fifth Normal Form)이라고 한다.  

>##### 무결성
>
> DB에 저장된 데이터 값이 그것이 표현하는 실제 세계의 값과 일치해야 한다는 DB의 성질을 의미한다. DB의 무결성을 유지하기 위해 DBMS는 연산에 제약을 두고 Transaction의 Atomicity, Consistency, Isolation, Durability를 보장한다. 무결성은 개체 무결성, 참조 무결성, 속성 무결성, 사용자 무결성, key 무결성으로 세분화할 수 있다.
{: .block-tip }

<br>

## 4. Snowflake schema ##

![](https://github.com/user-attachments/assets/c281d1c6-d6fe-404d-99b2-41b6443a3814)

Star schema의 Dimensional table 들은 필연적으로 이행 함수 종속성(Transansitive functional dependency)의 문제에 직면할 수 밖에 없다. 왜냐하면 특정 차원에 대한 모든 정보를 한 곳에 모아두기 때문이다. 앞서 살펴본 Star schema의 'Store' 차원 테이블의 사례에서도 'Id'에 의해 결정되는 Store_Number가 다시 Store_Province와 Country를 종속하고 있으므로 Store table, Province table, Country table로 분리할 경우 중복을 제거할 수 있음을 확인할 수 있다. 따라서 위에 제시된 사례처럼 각 차원 테이블의 이행 함수 종속성을 제거하여 3NF로 분리시킨 DW table model을 Snowflake schema라고 한다. 

Snowflake schema는 데이터 중복을 줄여주며 data load 시간이 단축된다는 장점이 있으나 join되는 relation의 개수가 증가하여 복잡성이 증가한다는 단점이 있다. Star schema와 Snowflake schema는 결국 단순화를 통해 DB의 성능을 향상시키고자 하는 '반정규화'와 중복을 제거하며 DB의 일관성과 무결성을 확보하고자하는 '정규화' 사이의 trade-off를 대표한다고 볼 수 있다. 즉, 정답이 존재하지 않는 문제이며 DB Engineer는 주어진 상황을 고려하여 적절한 정규화 단계를 선택해 DW를 설계해야 할 것이다.

<br>
<br>
<br>

