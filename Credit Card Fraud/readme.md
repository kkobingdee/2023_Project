# 신용카드 사기 거래 탐지 모델 개발

- **프로젝트 기간:** 2023.02 - 2023.06
- **사용 기술:** Python, Pandas, Scikit-learn, TensorFlow, Matplotlib, Seaborn
- **역할:** 데이터 전처리 및 모델 개발

## 프로젝트 개요
신용카드 거래 데이터를 분석하여 사기 거래를 탐지하는 모델을 개발했습니다. 데이터의 불균형 문제를 해결하고 여러 분류 알고리즘을 적용하여 성능을 비교한 후, 최적의 모델을 선정하여 사기 탐지 정확도를 높였습니다.

## 원시 데이터(credit_card_fraud) 구조
![dataset](https://github.com/user-attachments/assets/80a3e81a-3652-471e-a30d-95ce19c52e8a)
거래 시간(Time), 거래 금액(Amount), 기타 숨겨진 특성(V1-V28) 및 거래가 사기인지 여부를 나타내는 클래스(Class) 라벨 포함 총 31개의 특성으로 구성<br/><br/>
![data unbalance](https://github.com/user-attachments/assets/4dfa9c20-1f76-4723-be12-ce009c336a2c)<br/>
불균형(사기 거래: 0.17%, 정상 거래: 99.83%)이 매우 심함 <br/>

## 주요 작업 내용

### 데이터 전처리
- **특성 스케일링**: `Amount`와 `Time` 특성의 분포를 시각화하여 거래 금액과 시간의 일반적인 분포를 분석 후 Robust Scaler를 적용하여 데이터의 일관성을 확보하고 이상치의 영향을 최소화했습니다.<br/>
![amount and time](https://github.com/user-attachments/assets/47bdbf06-9263-44e5-92e2-089610cdad10)

### 데이터 불균형 문제 해결
- **언더샘플링**: 원본 데이터의 클래스가 불균형(사기 거래: 0.17%, 정상 거래: 99.83%)하여, Random Under Sampling을 통해 사기 거래와 정상 거래의 비율을 50:50으로 맞춘 샘플링된 데이터셋을 생성하였습니다.<br/>
![balanced data](https://github.com/user-attachments/assets/917653b3-1263-4ebc-a53d-b1706031c9ab)

### 시각화: 원본 데이터와 언더샘플링 후 데이터의 클래스 분포 비교
- 원본 데이터와 언더샘플링된 데이터의 클래스 분포를 시각화하여 데이터 불균형 문제 해결 전후의 분포를 비교하였습니다.

## 모델 개발 및 성능 평가

- **훈련 및 테스트 데이터 분할**: 데이터셋을 훈련 세트와 테스트 세트로 분할하여 모델 훈련과 평가를 준비했습니다.
- **모델 비교**: Logistic Regression, KNeighbors Classifier, Support Vector Classifier, Decision Tree Classifier의 4가지 모델을 비교하고, GridSearchCV를 통해 최적의 하이퍼파라미터를 탐색하였습니다.

### 모델 성능 평가
- **교차 검증 점수**: 최적의 모델에 대해 교차 검증을 수행하여 평균 정확도와 ROC AUC 점수를 기록하였습니다.
  
- **결과**:
  - Logistic Regression: 97.95%
  - KNeighbors Classifier: 93.63%
  - Support Vector Classifier: 97.48%
  - Decision Tree Classifier: 92.64%

  ![roc curve](https://github.com/user-attachments/assets/aade00e8-7eee-48b7-a55d-93fe8a1af982)

각 모델에 대한 ROC AUC 점수를 통해 성능을 확인하였으며, Logistic Regression이 가장 높은 점수를 기록했습니다.
