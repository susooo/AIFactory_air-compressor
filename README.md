# AIFactory -  ⚙️산업기기 피로도 예측
![image](https://github.com/susooo/AIFactory_air-compressor/assets/92291198/df66b868-3291-42c3-b827-74e1e7690068)

## 👍 리더보드 결과 공유
Goals : 피로도 증가 시 데이터 학습을 통해 산업기기 이상 전조증상을 예측하여 기기 고장을 예방하고 그로 인한 사고를 예방하는 모델 개발 <br>
public score : 0.9605793854 <br>
private score : 0.9542428615 <br>
<br>

## 📝 Introduction
대회 주제 : 산업기기 피로도를 예측하는 문제

[모델]

1. **비지도 학습(Unsupervised learning)** 방식으로 진행
2. 향후 **실시간 판정**에 활용되어야 하며 입력된 데이터를 **0(정상) 또는 1(이상)로 이진 분류**하는 모델
3. **시간 단위**로 생성되는 입력 데이터를 판정할 수 있는 모델


[평가 방법]
macro F1-Score

![image](https://github.com/susooo/AIFactory_air-compressor/assets/92291198/9c319826-bbf9-4112-9e91-059f1ad9c731)

## 📊 Data EDA
[데이터 확인]
* 데이터 분포 확인
* feature 연관성 확인
* 시계열 데이터 패턴 확인

[데이터 전처리]
* 데이터 범위 조절
* feature 범위 scaling
* feature 제거/추가

## 🔯 Isolation Forest
Isolation Forest는 Random Forest 알고리즘을 기반으로 하는 비지도 학습 방식의 이상치 탐지 알고리즘이다.

1. 훈련 데이터에서 무작위로 하나의 특성(feature)와 분할 값(split value)을 선택
2. 선택된 특성에 따라 분할 값을 기준으로 데이터를 두 개의 하위 집합으로 분리
3. 위의 과정을 반복하여 트리를 생성. 이후 각 데이터 포인트가 최종적으로 도달하는 노드까지의 경로 길이를 기록
4. 여러 개의 트리를 생성하여 Isolation Forest를 형성하고, 각 데이터 포인트의 평균 경로 길이를 계산
5. 평균 경로 길이가 짧은 데이터 포인트는 이상치로 판단

## 🔯 LSTM-AutoEncoder
LSTM-AutoEncoder는 이전 정보의 영향이 다음 정보에 영향을 주는 시계열 데이터의 처리에 효과적인 모델이다.
* 고차원의 시계열 데이터에서 효과적인 이상치 탐지 가능
*  Public : 0.7147570364

[한계]
1. long-term dependencies 문제를 효과적으로 처리 X -> attention을 활용한 transformer 모델 사용
2. train data는 정상 데이터로 구성, test data는 정상 데이터 및 이상 데이터로 구성 -> overfitting 모델링 방향 설정
3. overfitting 및 pre-trained 모델 -> TransAD or Anomaly Transformer 모델 사용

## 🔯 Anomaly Transfomer
Anomaly Transformer를 선택한 이유는 지역적 시계열 특징과 전반적 시계열 특징을 결합하여 더욱 정확한 이상치 탐지를 제공하고, 기존 RNN 기반 방법론에서 발생하는 이상치 데이터가 묻히는 문제를 개선하여 시계열 데이터 분석 성능을 향상시키기 때문이다.
1. Vanila Anomaly Transformer 적용
* Public - 0.6092 / Total - 0.6038

2. PSM 데이터셋 Pre-trained model 사용
* PSM dataset으로 pre-train한 model 사용
* Public - 0.7889 / Total - 0.7849

3. HP(마력) feature 추가 및 전체 데이터셋 학습
*  설비번호별로 학습하던 것을 HP(마력) feature를 추가하여 전체 데이터 셋을 학습하는 것으로 변경
*  Public - 0.9040 / Total - 0.9002

4. 최종 모델
* HP별 hyper-parameter tuning set 설정 -> anormaly ratio, window size, shuffle 변경
* Public - 0.9606 / Total - 0.9542

## 💫 SOTA Visualization
![image](https://github.com/susooo/AIFactory_air-compressor/assets/92291198/86d7c824-74f4-4994-b40b-0de3133280a0)
![image](https://github.com/susooo/AIFactory_air-compressor/assets/92291198/dbffac24-d88e-4644-984a-6dc7aeb224ee)
![image](https://github.com/susooo/AIFactory_air-compressor/assets/92291198/b378a4ce-3c88-4660-873f-e333da6b4526)
![image](https://github.com/susooo/AIFactory_air-compressor/assets/92291198/2472aaaa-2587-4570-8a1d-8e3b1c6b74d5)





