# Insurance
## 의료비 예측하기
프로젝트 기간: 2024/08/01(목) ~ 2024/08/08(목)  
<br/>
## 개요
이 프로젝트는 건강 보험 청구 데이터를 기반으로, 다양한 회귀 모델을 사용하여 건강 보험에 청구하는 개인 의료비를 예측하는 것을 목표로 합니다. 사용된 데이터셋은 미국 내 건강 보험 수혜자들의 나이, 성별, 신체질량지수(BMI), 자녀 수, 흡연 여부, 지역 정보를 포함하고 있으며, 각 수혜자에 대한 의료비도 포함되어 있습니다.  

프로젝트의 목표는 다음과 같습니다.
1. 의료비를 정확히 예측할 수 있는 모델을 구축하여 보험 상품의 가격 책정에 대한 명확한 통찰력을 제공.
2. 건강 보험 데이터에서 유의미한 패턴과 변수 간의 관계를 발견함으로써 보험사의 데이터 기반 의사결정을 지원.
3. 분석 결과와 모델 성능을 시각적으로 표현하여 이해관계자들에게 효과적으로 전달.

이 프로젝트를 통해 의료비를 정확히 예측할 수 있는 모델을 구축하여 보험 상품의 가격 책정에 대한 깊은 통찰력을 제공하고, 건강 보험 데이터에서 유의미한 패턴과 변수 간의 관계를 발견하여 보험사의 데이터 기반 의사결정에 도움되고자 합니다. 또한, 예상치 못한 의료 비용이 부담이 될 수 있는 상황에서 수혜자들이 더 효과적으로 재정을 계획하고 관리할 수 있도록 돕기 위해 이 프로젝트를 진행하게 되었습니다.
<br/>
## 사용한 데이터셋
insurance.csv
<br/>

## 프로젝트 목록
1. 데이터 로딩 및 시각화
2. PyCaret을 이용한 모델 비교
3. 모델 학습 및 평가
4. 하이퍼파라미터 최적화
5. 스태킹
6. 딥러닝 모델
7. TabNet 모델

## 프로젝트 수행 과정
1. 데이터 로딩 및 시각화
    - 데이터셋을 로드하고 결측값을 확인하였습니다.
    - 나이, BMI, 자녀 수, 보험료와 같은 수치형 변수와 성별, 흡연 여부, 지역 등 범주형 변수의 분포를 시각화하였습니다.
    - 상관 행렬을 시각화하여 수치형 변수 간의 관계를 조사하였습니다.

2. PyCaret을 이용한 모델 비교
    - PyCaret을 활용해 데이터를 설정하고 다양한 회귀 모델을 RMSE를 기준으로 비교하였습니다.
    - 최상위 모델을 저장하고 다운로드하였습니다.

3. 모델 학습 및 평가
    - Gradient Boosting, LightGBM, Random Forest 회귀 모델을 수동으로 학습시키고, RMSE와 R² 점수를 사용해 평가하였습니다.
    - 실제 값과 예측값을 비교하는 산점도를 사용하여 모델 성능을 시각화하였습니다.

4. 하이퍼파라미터 최적화
    - Bayesian Optimization을 활용하여 Gradient Boosting, LightGBM, Random Forest 모델의 최적 하이퍼파라미터를 찾았습니다.
    - 최적의 하이퍼파라미터와 성능 지표를 확인하였습니다.

5. 스태킹
    - Gradient Boosting, LightGBM, Random Forest를 기본 모델로 하고, Gradient Boosting Regressor를 메타 모델로 사용하는 스태킹 회귀 모델을 구현하였습니다.
    - 이 모델을 평가하고 성능을 시각화하였습니다.

6. 딥러닝 모델
    - TensorFlow/Keras를 사용하여 신경망을 구축하고 학습하였습니다.
    - Keras Tuner를 사용해 하이퍼파라미터를 최적화하고, 훈련 및 검증 손실을 시각화하였습니다.
    - 모델 체크포인팅을 구현하여 검증 손실을 기준으로 최상의 모델을 저장하였습니다.

7. TabNet 모델
    - TabNet 모델을 사용하여 테이블 데이터에 특화된 주의 메커니즘을 활용하였습니다.
    - TabNet 모델을 학습시키고 RMSE와 R² 점수로 성능을 평가하였습니다.

## 모델의 test dataset에 대한 R2 Score (소수점 다섯째 자리에서 반올림) 
| Model | R2 Score |
|:--------------------------|:-------|
| GradientBoostingRegressor | 0.8802 |
| LightGBMRegressor         | 0.8760 |
| RandomForestRegressor     | 0.8748 |
| Stacking                  | 0.8655 |
| Multi-Layer Perceptron    | 0.8582 |
| TabNetRegressor           | 0.7426 |

## 최종 모델
GradientBoostingRegressor
- test dataset에 대한 결과
  - RMSE: 약 4311.7676
  - R2 Score: 약 0.880248

## 결론
**GradientBoostingRegressor**: 하이퍼파라미터 최적화 후 RMSE가 4329.21에서 4311.77로, R² Score가 0.8793에서 0.8802로 향상되며, 최종적으로 가장 높은 성능을 기록함.

**LightGBMRegressor, RandomForestRegressor, Stacking**: GradientBoostingRegressor와 비교했을 때 상대적으로 낮은 성능을 보임.

**Keras-Tuner를 이용한 딥러닝 하이퍼파라미터 최적화**: 여전히 GradientBoostingRegressor와 같은 머신러닝 모델에 비해 성능이 미치지 못함. 이는 정형 데이터에서 딥러닝 모델의 성능이 제한적일 수 있음.

**TabNetRegressor**: RMSE가 6321.47로 가장 높고, R² Score는 0.7426으로 가장 낮음. 이는 정형 데이터에서 딥러닝 기반 모델의 성능이 기대 이하였으며, 데이터 수가 부족해 딥러닝 모델이 최적의 성능을 발휘하지 못했을 가능성이 있음.

## 향후 보안할 점
**데이터 수와 특성 부족**: 데이터 수가 부족하고 의료 관련 특성이 단순하다는 점이 아쉬웠습니다. 새로운 특성을 추가하고 피처 간의 상호작용을 고려하면 모델의 예측 성능을 향상될 것입니다.

**Feature Importance 분석**: 모델이 어떤 특성에 의존하는지 파악하기 위한 Feature Importance 분석이 부족했습니다. 이를 통해 중요 특성을 강조하고 불필요한 특성을 제거하면 모델 성능이 더욱 개선될 것입니다.

**한국 실정 반영**: 미국 의료 기반 시스템으로 측정된 의료비 데이터를 한국 실정에 맞게 소득분위 및 보험료 분석을 추가하면, 가계 재정에 대한 실질적인 인사이트를 제공하여 분석의 유용성이 높아질 것입니다.
