# Solar power prediction
## Description
  * 신재생 에너지 태양광 발전량 예측을 위한 시계열 데이터 분석 기법 발굴하기
  * 신재생 에너지 관리 솔루션 개발 활용 및 에너지 서비스 산업 발전 촉진함
  * 향후 2일 동안의 30분 간격의 태양광 발전량 예측하기

## Data
* **Dataset**
  * 3년 간의 태양광 발전량 데이터
  * 30분 마다 한 번씩 측정됨
  * 시간(Day, Hour, Minute), DHI, DNI, WS, RH, T, TARGET으로 이루어짐

* **Pre-processing**
  * 각 계절마다 공통적으로 해가 뜨지 않는 시간(0:00 ~ 4:00, 19:30 ~ 23:30)에는 태양광 발전량이 0이므로 이 시간을 제외함
  * 각 계절마다 공통적으로 해가 뜨는 시간(4:30 ~ 19:00)만 추출함
    * 하루에 총 48개의 데이터(0:00 ~ 23:30)에서 30개(4:30 ~ 19:00)만 추출함
  * TARGET으로만 학습했을 때의 성능이 가장 잘 나와서 TARGET 외의 모든 열을 drop 함
  * MinMaxScaler를 사용


## Model
* **Train Model**
  * LSTM, Bidirectional LSTM, CNN 모델을 사용하여 Ensemble Model로 바꿈

* **Hyperparameter**
  * 입력 길이 : 3일 간의 TARGET 데이터
  * 예측 길이 : 2일 간의 TARGET 데이터
  * Epoch: 15,000
  * Learning rate : 0.001
  * hidden layer units : [10, 10]
  * Activation : selu


## Performance
* Pinball Loss로 심사함
  ![image](https://github.com/Silinu1016/Competition/assets/97217295/ea360ddd-c6d2-4844-9bde-4e0dfa8278a5)
  * τ: 퀀타일 값 (0.1, 0.2, 0.3, 0.4, 0.5, 0.6, 0.7, 0.8, 0.9)
	* y: 실제 값
	* z: 퀀타일 예측값
	* Lτ: pinball loss 함수
* 결과
  * 9.5 → 1.75까지 Loss를 줄여 Public 기준 7등함.
  ![image](https://github.com/Silinu1016/Competition/assets/97217295/0a55b60d-8023-4960-8ca7-2c67e0674e84)

