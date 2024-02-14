# Jeju special product price prediction
## Description
  * 제주도 특산물의 안정적이고 효율적인 수급을 위해서 해당 특산물들의 가격에 대한 정확한 예측이 필요함
  * 제주도 특산물의 가격을 예측하는 AI 모델 개발하기

## Data
* **Dataset**
  * ID, timestamp, item, corporation, location, supply, price로 이루어짐

* **Pre-processing**
  * 일요일을 0으로 바꿨을 때 점수가 좋게 나와 일요일 = 0이라는 것에 초점을 둠
  * price에만 MinMaxScaler를 적용함


## Model
* **Train Model**
  * Autogluon 모델을 사용함

* **Hyperparameter**
  * 입력 길이 : 48일 간의 데이터
  * 예측 길이 : 28일 간의 price 데이터
  * Eval_metric: RMSE
  * Random Seed: 16


## Performance
* RMSE로 심사함

* 결과
  * 1937 → 667까지 Loss를 줄여 Public 기준 상위 10%를 달성함.
