# EDA 보고서

## 주제: 헬스장 회원 분석

## 1. 헬스장 회원 데이터의 소개 및 분석 방향
    1. **데이터 출처: Kaggle**
    (https://www.kaggle.com/datasets/valakhorasani/gym-members-exercise-dataset)
        - 해당 데이터셋은 헬스장 회원의 운동 루틴, 신체적 특징, 피트니스 지표에 대한 자세한 개요를 제공
        - 심박수, 소모 칼로리, 운동 기간과 같은 핵심 성과 지표뿐만 아니라.
        - 각 항목에는 인구 통계 데이터, 경험수준도 포함되어 있어 피트니스 패턴, 건강 추세에 대한 포괄적 분석 가능
    
    2. **탐색 목적**: 헬스장 회원들의 정보를 바탕으로 아래의 4가지 주제로 탐색적 자료분석을 하고자 함
        1) 운동종류에 따른 심박수 간의 상관관계
        2) (물 섭취, 체지방량)과 칼로리 소모 관계와 상관성을 분석
        3) 운동빈도수와 수행되는 운동유형이 체지방비율에 미치는 영향
        4) 연령대별 운동 선호도 및 그에 따른 칼로리 소모량

## 2. 데이터 소개
헬스장 회원 데이터는 회원의 인구통계 정보와 운동습관, 심박수 등을 포함하며 주요 컬럼은 다음과 같습니다.
  - Age: 나이
  - Gender: 성별
  - Weight (kg): 체중
  - Height (m): 키
  - Max_BPM: 최대 심박수
  - Avg_BPM: 평균 심박수
  - Resting_BPM: 휴식 시 심박수
  - Session_Duration (hours): 운동 시간(시간 단위)
  - Calories_Burned: 소모 칼로리
  - Workout_Type: 운동 종류
  - Fat_Percentage: 체지방률
  - Water_Intake (liters): 수분 섭취량(리터)
  - Workout_Frequency (days/week): 주간 운동 빈도
  - Experience_Level: 운동 경력
  - BMI: 체질량지수 (BMI)

## 3. 주제별 자료분석 및 해석
   1. 운동종류에 따른 심박수 간의 상관관계: https://github.com/encore-ai-240909/eda_workspace/blob/master/Team2/EDA/README_01.md
   2. (물 섭취, 체지방량)과 칼로리 소모 관계와 상관성을 분석: https://github.com/encore-ai-240909/eda_workspace/blob/master/Team2/EDA/README_02.md
   3. 운동빈도수와 수행되는 운동유형이 체지방비율에 미치는 영향: https://github.com/encore-ai-240909/eda_workspace/blob/master/Team2/EDA/readme%EC%9C%A0%EC%98%81%EC%A4%80.ipynb
   4. 연령대별 운동 선호도 및 그에 따른 칼로리 소모량: https://github.com/encore-ai-240909/eda_workspace/blob/master/Team2/EDA/soovin_README.md

## 4. 결론
    - 각 팀원별 컬럼 간 유의미한 결과를 도출하기 위해 4가지 주제로 개별 분석 진행
    - 다수의 분석 결과, 데이터 간 유의미한 상관관계를 도출하지 못하였음
    - 컬럼 간에 독립적으로 변화하는 특성을 가진 데이터가 많다는 점을 시사함
    - 상관관계가 높은 데이터를 추가적으로 분석함이 필요