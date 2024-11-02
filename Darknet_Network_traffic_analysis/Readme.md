# 다크넷 네트워크 트래픽 분석 및 비정상 트래픽 탐지

- **프로젝트 기간:** 2023.07 – 2023.12
- **사용 기술:** Python, Pandas, Scikit-learn, TensorFlow, Keras, Matplotlib
- **역할:** 데이터 전처리 담당

## 프로젝트 개요
다크넷 트래픽 데이터를 분석하여 비정상 트래픽을 탐지하고, 네트워크 보안을 강화하기 위한 예측 모델을 개발했습니다. 연구실 퇴사로 최종 모델 개발은 직접 진행하지 못했으나, 전처리를 통해 특성 추출과 데이터 불균형 문제 해결에 집중했습니다.

## 원시 데이터(Darknet.csv) 구조
![원시데이터 2](https://github.com/user-attachments/assets/f923b9e8-f144-49fc-ae3e-de9f92c98bee)
출발지와 목적지 IP, 포트 번호, 프로토콜, 트래픽 시간 등의 비정상 트래픽 탐지를 위한 85개의 특성으로 구성.

## 주요 작업 내용

### 데이터 전처리
- **결측치 처리 및 정규화**: `Flow Bytes/s` 등 결측치가 포함된 특성들을 제거하고, 주요 수치형 변수들을 표준화하여 데이터의 일관성을 확보했습니다. `np.inf`와 `-np.inf` 값을 `NaN`으로 대체하여 결측치로 처리했습니다.

### 특성 생성
- **시간대별 트래픽 분포**: `Timestamp`에서 `hour`를 추출하여 특정 시간대에 집중되는 트래픽을 파악했습니다.
  ![timestamp](https://github.com/user-attachments/assets/e370b288-e038-4e67-ab34-bd29682238cc)

- **IP 기반 특성**: 소스 및 목적지 IP에서 1-gram, 2-gram, 3-gram 특성을 생성하여 패턴을 분석했습니다.
  ![N-grams](https://github.com/user-attachments/assets/297d89b1-8f85-4231-a80f-97e0a2c81cce)
- **국가 정보 및 보곤 IP 여부**: IP에서 국가 정보를 추출하고 보곤 IP 여부를 추가하여, 지리적 위치와 비정상 활동 간의 연관성을 확인했습니다.
<br/><br/>

## 분석

### 시간대별 트래픽 양
- **분석 결과:** 일반 트래픽과 다크넷 트래픽이 시간대에 따라 다른 패턴을 보입니다. 특정 시간대에 다크넷 트래픽이 더 활발할 경우 이상 활동 가능성을 시사할 수 있습니다. <br/>
![hours](https://github.com/user-attachments/assets/26e74c2d-a5a9-4fde-9318-13fc1e89c0db)

---

### 트래픽 특성화
#### 일반 트래픽 유형
- **분석 결과:** 일반적으로는 다른 유형들에 비해 P2P 타입과 Browsing 타입이 많습니다.
![clearnet](https://github.com/user-attachments/assets/093a591a-2c64-4924-83a1-3138ba01978f)
#### 다크넷 트래픽 유형
- **분석 결과:** 다크넷 트래픽의 세부 유형에는 Audio-Streaming 타입이 압도적으로 많습니다.
![darnet](https://github.com/user-attachments/assets/62f65780-978b-425a-8521-2bc166306f97)

---
