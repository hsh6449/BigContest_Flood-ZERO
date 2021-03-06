# 빅콘테스트 : 홍수 유입량 예측
## Overview(FeedBack)
- JBIG 멤버들과 함께 준비한 2번째 대회
- 주어진 데이터를 이해하는 것이 약간 어려웠음, 수위와 강우량이 어떻게 측정되어있는지 설명이 모호했음
- 또한 데이터 집단이 6개로 나뉘어져 있었는데 다같이 학습시키기엔 과적합이 발생하여 6개 데이터 집단이 의미하는 것을 알기 어려웠음 
- 어떤 모델이 가장 효과적일지, 데이터를 어떻게 처리해야 효과적일지 충분히 고민했었던 대회
- 결과는 예선 탈락

## ROLE
- `황산하` : PPT제작, 모델링, 전처리
- `고경수` : Feature engineering
- `문우혁` : Feature engineering, 하이퍼파라미터 튜닝


# 1. Data Split

- 홍수사상의 데이터에서 유입량을 예측하는 데이터인데 train set과 test set을 미리 나눠놓기라도 한듯 어느 시점부터는 유입량이 비어있어서 train,test set으로 나눴다.
- 또한 같은 유입량에 대하여 데이터 집단이 6개로 나뉘기 때문에 이를 고려하여 한 행의 데이터를 집단별로 나눴다.
- 집단을 모두 합쳐 학습을 진행하면 과적합 발생이 의심

# 2. Data Preprocessing & EDA
![image](https://user-images.githubusercontent.com/57973170/153583423-a789fb1b-2987-447d-bd75-e363f623ab9c.png)
- 홍수 사상번호 별로 강우량과 수위가 시간의 데이터를 포함한다고 판단하여 시간의 경향을 반영하기 위해 인덱스를 정규화해서 새로운 파생변수로 넣었음
- 과적합이 의심 되기 때문에 집단을 각각 따로 학습을 시킨 후 RMSE가 가장 낮은 집단을 이용
- 데이터간 상관관계가 매우 높아 다중 공선성이 의심

# 3. Data modeling
- CatBoost를 이용

![image](https://user-images.githubusercontent.com/57973170/153584571-b2907c96-a016-4e44-b120-0c58416f030f.png)
