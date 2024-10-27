## int's EDA_Workspace
# INT*'s EDA_Workspace*

## 1. 서론: MBA 데이터 소개 및 분석 방향

1. **데이터 출처**: [MBA Admission dataset, Class 2025 (Kaggle)](https://www.kaggle.com/datasets/taweilo/mba-admission-dataset)

2. **MBA 데이터**: 2025년 와튼스쿨 MBA 지원자 정보와 합격 여부를 기록한 자료

3. **분석 방향**: MBA 데이터에 대하여 아래의 주제로 탐색적 자료분석(EDA)을 수행
   - 지원자 정보에 따른 **MBA 합/불여부 예측** (분류)
   - 합/불 여부에 영향을 미치는 **주요 특성 탐색**

## 2. 데이터 소개

### 1. **Data Source:**
   - Synthetic data generated from Wharton Class of 2025's statistics.

### 2. **Meta Data**:
   - `application_id`: Unique identifier for each application
   - `gender`: Applicant's gender (Male, Female)
   - `international`: International student (TRUE/FALSE)
   - `gpa`: Grade Point Average (on a 4.0 scale)
   - `major`: Undergraduate major (Business, STEM, Humanities)
   - `race`: Racial background (White, Black, Asian, Hispanic, Other / null: international student)
   - `gmat`: GMAT score (800 points)
   - `work_exp`: Years of work experience
   - `work_industry`: Industry of previous work experience (Consulting, Finance, Technology, etc.)
   - `admission`: Admission status (Admit, Waitlist, Null: Deny)

### 3. **Usage**:
   - **Exploratory Data Analysis (EDA)**: Understand distributions, relationships, and patterns.
   - **Classification**: Predict admission status based on other features.

## 3. 자료 분석 및 해석

### 3-1. 전공 / 산업 별 지원자 수
   - 전공별 지원자 수 확인: Humanities(2481명), Business(1838명), STEM(1875명)  
   - **차트**: 전공별 지원자 분포 그래프 첨부

### 3-2. 인종 및 국제학생 여부에 따른 지원자 수
   - 백인 지원자 가장 많음, 국내 학생이 국제 학생보다 약 2.36배 많음  
   - **차트**: 인종 및 국제학생 분포 그래프 첨부

### 3-3. 업무 경험 연차 별 지원자 수
   - 평균 업무 연차는 약 5년이며, 4~6년 차 지원자가 다수  
   - **차트**: 업무 경험 연차별 지원자 수 히스토그램 첨부

### 3-4. GPA, GMAT 점수 - 합격 여부
   - GPA와 GMAT 점수 분포를 통한 합격 여부 분석  
   - **차트**: GPA 및 GMAT별 합격 여부 Box Plot, Histogram 첨부

### 3-5. 연관성 분석
   - **히트맵**: 변수 간 상관 계수를 시각화하여, 합격 여부에 대한 주요 특성을 탐색. 상관성이 낮아 여러 특성의 조합이 중요한 것으로 해석 가능

## 4. 결론

### 4-1. **분석 결과 요약**
   - **핵심 결과**: 단일 특성보다는 여러 특성의 조합이 MBA 합격 여부에 중요한 영향을 미침
   - **주요 성과**: GPA와 GMAT의 상관 계수는 0.58로 다소 낮아 합격 여부에 독립적인 특성으로 작용할 가능성 있음

### 4-2. **기존 분석 대비 새로운 해석 및 의미**
   - 기존 중요 특성인 GMAT과 GPA의 절대적 영향력이 크지 않음을 확인
   - **의미**: 지원자의 다양한 특성 조합이 합격 여부에 복합적인 영향을 미침을 시사

### 4-3. **분석에서의 제약사항**
   - Waitlist를 거절로 간주한 점이 결과에 영향을 줄 가능성
   - 국제 학생 여부로 인종 변수가 null 처리된 점은 분석에 있어 제약이 될 수 있음

### 4-4. **추가 분석의 필요성 및 의미**
   - 다차원 데이터를 고려한 머신러닝 모델 적용 필요성 제안
   - 다중 특성을 반영한 심화 분석이 합격 예측 모델에 큰 기여를 할 수 있을 것으로 기대됨

---

## 데이터 전처리

1. **데이터 구조 및 기초통계 파악**
2. **불필요한 column 삭제**: `application_id`, `international`
3. **결측치 처리**: `admission`의 null을 decline(거절)로 대체
4. **이상치 탐색**: `admission`의 Waitlist를 거절로 간주
5. **범주형 특성 인코딩**
   - **Label Encoding**: gender
   - **One-hot Encoding**: major, race, work_industry
6. **변수들 간의 관계 파악**: 상관 계수, 산점도, 히스토그램 등 시각화 사용
7. **변수 구간화 (범주화)**: work_exp → 3개의 구간으로 분할 (1~3, 4~6, 7~9)

---

## 훈련

1. **스케일링**
   - StandardScaler로 특성값을 표준화하여 모델 성능 최적화

2. **교차검증**
   - cross_val_score를 통해 모델 신뢰도를 높이고 과적합 방지

3. **특성공학**
   - PolynomialFeatures로 2차원 특성을 생성하여 다차원 데이터를 학습 가능

4. **훈련모델 선택**
   - DecisionTree를 사용하여 빠른 훈련과 높은 정확도 확보

5. **하이퍼파라미터 튜닝**
   - GridSearchCV를 통해 DecisionTree의 `max_depth`, `min_sample_split`, `min_sample_leaf`를 최적화

---

### 자료 분석 및 해석

- 결과를 통해 예측 모델 구축에 기여할 수 있는 인사이트 도출
