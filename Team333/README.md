
<!--이예진 start-->
# ⚾ 야구선수(타자)들의 데이터로 OPS예측하기 ⚾

## 1. Introduction (소개)
* **목적** : 야구 선수(타자)들의 포지션, 경기수, 타석, 점수, 안타, 2루타, 3루타, 홈런, 타점, 볼넷, 삼진, 도루, 도루실패, 타율, 출루율, 장타율 데이터로 OPS를 예측한다.
* **데이터 출처** : Kaggle. [MLB Player Seasons Data (1876 - 2024)](https://www.kaggle.com/datasets/logancuster/baseball-seasons-data)

## 2. Data Overview (데이터 개요) - `mlb_df`

### 2-1) 데이터 형태
`mlb_df.shape` : **( index : 57121, column :17 )**

### 2-2) 변수 설명

| 컬럼명                   | 데이터 타입               | 설명                           |
|-----------------------|---------------------------|--------------------------------|
| season                | 수치형(이산형)           | 시즌                           |
| first_name            | 문자형                   | 성                             |
| last_name             | 문자형                   | 이름                           |
| link                  | 문자형                   | 링크                           |
| position              | 문자형(범주형)           | 포지션                         |
| team                  | 문자형(범주형)           | 팀                             |
| games_played          | 수치형(이산형)           | 경기수                        |
| at_bats               | 수치형(이산형)           | 타석                          |
| runs                  | 수치형(이산형)           | 점수                          |
| hits                  | 수치형(이산형)           | 안타                          |
| doubles               | 수치형(이산형)           | 2루타                        |
| triples               | 수치형(이산형)           | 3루타                        |
| homeruns              | 수치형(이산형)           | 홈런                          |
| rbi                   | 수치형(이산형)           | 타점                          |
| walks                 | 수치형(이산형)           | 볼넷                          |
| strikeouts            | 수치형(이산형)           | 삼진                          |
| stolen_bases          | 수치형(이산형)           | 도루                          |
| caught_stealing       | 수치형(이산형)           | 도루 실패                     |
| batting_average       | 수치형(연속형)           | 타율                          |
| on_base_percentage    | 수치형(연속형)           | 출루율                        |
| slugging_percentage   | 수치형(연속형)           | 장타율                        |
| on_base_plus_slugging | 수치형(연속형)           | OPS                            |

| 포지션 코드 | 포지션 설명                             |
|-------------|----------------------------------------|
| X           | 시즌 중 팀 전환                        |
| C           | 포수 (Catcher)                        |
| 3B          | 3루수 (Third Baseman)                 |
| 2B          | 2루수 (Second Baseman)                |
| P           | 투수 (Pitcher)                        |
| 1B          | 1루수 (First Baseman)                 |
| SS          | 유격수 (Shortstop)                    |
| DH          | 지명타자 (Designated Hitter)          |
| RF          | 우익수 (Right Field)                  |
| LF          | 좌익수 (Left Field)                   |
| CF          | 중견수 (Center Field)                 |
| PH          | 대타 (Pinch Hitter)                   |
| OF          | 외야수 (OutFielder)                   |
| PR          | 대주자 (Pinch Runner)                 |




### 2-3) 간단한 요약 

| **Metric**             | **Minimum** | **Q1**   | **Median (Q2)** | **Q3**   | **Maximum** |
|------------------------|-------------|----------|-----------------|----------|-------------|
| **Position**           | 0           | 2.0      | 3.0             | 6.0      | 11          |
| **Games Played**       | 1           | 26.0     | 76.0            | 126.0    | 165         |
| **At Bats**            | 0           | 65.0     | 218.0           | 431.0    | 716         |
| **Runs**               | 0           | 7.0      | 26.0            | 56.0     | 177         |
| **Hits**               | 0           | 14.0     | 54.0            | 114.0    | 262         |
| **Doubles**            | 0           | 2.0      | 9.0             | 19.0     | 67          |
| **Triples**            | 0           | 0.0      | 1.0             | 3.0      | 36          |
| **Home Runs**          | 0           | 0.0      | 2.0             | 8.0      | 73          |
| **RBI**                | 0.0         | 6.0      | 23.0            | 50.0     | 191.0       |
| **Walks**              | 0           | 5.0      | 17.0            | 37.0     | 232         |
| **Strikeouts**         | 0.0         | 12.0     | 36.0            | 53.0     | 223.0       |
| **Stolen Bases**       | 0.0         | 0.0      | 2.0             | 6.0      | 130.0       |
| **Caught Stealing**    | 0.0         | 0.0      | 2.45            | 2.45     | 42.0        |
| **Batting Average**    | 0.0         | 0.216    | 0.253           | 0.284    | 1.0         |
| **On-Base Percentage** | 0.0         | 0.279    | 0.317           | 0.353    | 1.0         |
| **Slugging Percentage**| 0.0         | 0.288    | 0.36            | 0.427    | 3.0         |
| **OPS**                | 0.0         | 0.579    | 0.679           | 0.774    | 4.0         |


## 3. Data Cleaning (데이터 전처리)
### 3-1) 결측치 처리 및 데이터 변환
```
# 결측치 처리 및 데이터 타입 수정이 필요해 보이는 컬럼
# strikeouts,rbi, stolen_bases, caught_stealing, on_base_percentage,on_base_plus_slugging

columns = ['strikeouts','rbi', 'stolen_bases', 'caught_stealing', 'on_base_percentage','on_base_plus_slugging']

for i in range(len(columns)):
    column = columns[i]
    mlb_df[column] = pd.to_numeric(mlb_df[column],  errors='coerce')
    rbi_mean = mlb_df[column].mean()
    mlb_df[column] = mlb_df[column].fillna(rbi_mean)
    print(mlb_df[column].describe())
```


### 3-2) 필요없는 데이터/컬럼 제거
```
# 포지션 P(투수) 인덱스 제거 
    - 야수들 데이터만 있게 하고 싶어서.
    
drop_position = ['P', 'X']
for i in range(len(drop_position)):
    mlb_df = mlb_df[mlb_df['position'] != drop_position[i]]
```
```
# 시즌, 선수 이름, 팀은 OPS를 예측에 필요 없는 데이터로 판단. 

columns = ['season', 'first_name', 'last_name', 'link','team']

mlb_df = mlb_df.drop(columns, axis=1)
```
## 4. Univariate Analysis (단일 변수 분석)
### 4-1) 수치형 변수 분석
```
columns =['games_played', 'at_bats', 'runs', 'hits', 
    'doubles','triples', 'homeruns', 'rbi', 
    'walks', 'strikeouts', 'stolen_bases','caught_stealing', 
    'batting_average', 'on_base_percentage','slugging_percentage','on_base_plus_slugging']
```
- **BoxPlot**
![mlb_df_boxplot.png](png%2Fmlb_df_boxplot.png)

- **HistPlot**
![mlb_df_histplot.png](png%2Fmlb_df_histplot.png)

### 4-2) 범주형 변수 분석
`mlb_df['position']`
![position_barplot.png](png%2Fposition_barplot.png)

## 5. Bivariate Analysis (두 변수 간 관계 분석)
### 5-1) 수치형-수치형 관계
- **Heatmap**
![mlb_df_heatmap.png](png%2Fmlb_df_heatmap.png)

- **RegPlot ( 산점도 + 회귀선 )**
![mlb_df_regplot.png](png%2Fmlb_df_regplot.png)


## 6. 데이터 분할 및 예측
- 데이터 예측을 위해 훈련/테스트 데이터 분할 및 스케일링 후 모델의 성능을 더 정확하게 평가하고 일반화 능력을 높이기 위해서 5-fold 교차검증을 해보았습니다.
```
각 회차 MSE 점수: [0.00035387 0.00036867 0.0002685  0.00038115 0.00036077]
각 회차 MAE 점수: [0.00470781 0.00490386 0.00440818 0.00500197 0.00487834]
각 회차 R² 점수: [0.99269182 0.99231072 0.99432779 0.99190442 0.99199767]

[최종점수]
MSE 점수 : 0.0003465917698958586
MAE 점수 : 0.004780029937705997
RMSE 점수 : 0.0186169753154442
R² 점수 : 0.9926464854335595
```

이번 모델의 최종 MSE와 MAE는 각각 0.00035와 0.00478로, 낮은 수치를 보였습니다. 이는 예측값과 실제값 사이의 오차가 매우 작음을 의미합니다. 또한 R² 점수는 0.993으로, 거의 1에 가까워 모델이 데이터를 잘 설명한다는 것을 나타냅니다. 이를 통해 모델이 높은 정확도로 예측할 수 있음을 확인할 수 있었습니다.

- **모델 적용**

3차 다항 변환과 선형 회귀를 결합한 파이프라인 모델 적용
```
훈련 : 0.996015928713019 
  -> 모델이 훈련 데이터에 대해 높은 예측 정확도를 가지고 있다.
테스트 : 0.9950869345372476
  -> 모델이 테스트 데이터에서도 매우 높은 성능을 유지하고 있어, 과적합(overfitting) 문제가 거의 없다.

[최종점수]
MSE 점수 : 0.00022476399949987862,
MAE 점수 : 0.005854154969597924,
RMSE 점수 : 0.014992131252756514,
R² 점수 : 0.9950869345372476
```
따라서 모델이 새로운 데이터에 대해서도 안정적인 예측을 할 가능성이 크다.

- **예측**

대표적으로 데이터 1개를 사용해 자동화된 예측 값과 실제 수식적으로 예측한 값이 같은지 알아보았습니다.
```
직접 계산 :     0.6486099670385952, 
model.predict : 0.6486099670385952
```



<!-- 이예진 end -->


<!-- 김해빈 start -->

# ❤️Instagram post 데이터로 Likes 예측하기❤️

## 1. 데이터 로드
- **목적** : 데이터 목적, 컬럼 정의서가 미존재하는 데이터를 분석하여 의미를 도출해보자!
- **데이터 출처**: Kaggle [1100 Instagram Users Datetime Posts Data](https://www.kaggle.com/datasets/vasileiosmpletsos/1100-instagram-users-datetime-posts-data/data)

## 2. 데이터 구조 및 기초 통계 확인
- `df.shape` : **(178922, 13))**


- `df['User uuid'].unique()` : array([   1,    2,    3, ..., 1087, 1088, 1089], dtype=int64)

  - 실제 데이터 확인 시, **1089명의 id**로 구성된 데이터임을 확인


- `df.info()`:

| # | Column                | Non-Null Count | Dtype   |
|---|-----------------------|----------------|---------|
| 0 | User uuid             | 178922         | int64   |
| 1 | Likes                 | 178922         | int64   |
| 2 | Days passed from post | 178922         | int64   |
| 3 | Likes Score           | 178922         | float64 |
| 4 | Type                  | 178922         | object  |
| 5 | Numer of Tags         | 178922         | int64   |
| 6 | Numer of Comments     | 178922         | int64   |
| 7 | Date Posted           | 178922         | object  |
| 8 | Year                  | 178922         | int64   |
| 9 | Month                 | 178922         | int64   |
| 10| Day                   | 178922         | int64   |
| 11| Hour                  | 178922         | int64   |
| 12| Minute                | 178922         | int64   |

> 'Likes Score'가 어떻게 도출된 값인지 명시되지 않음 !!

## 3. 결측치 및 이상치 탐색 & 데이터 시각화를 통한 탐색 & 데이터 정제 및 전처리

![instagram_boxplot.png](PNG/instagram_boxplot.png)

> "Days passed from past"가 데이터 평균보다 유난히 큰,<br>"Year"가 데이터 평균보다 유난히 작은 데이터가 boxplot을 넘어감

### 3-1) 'Likes'와 'Likes Score' 간 상관관계 확인

- 직접 사용자별로 정규화 후 평균의 차이 확인 시, 평균의 차이가 0.039로 거의 일치함.
- `df['Likes Score'].corr(df['Likes_Normalized_By_User'])`= 0.97로 Pearson 상관계수 상 "매우 높은 상관관계"에 해당함
- 'Likes Score'는 **사용자별로 Likes를 정규화한 값** 임을 확인

```
user = df.groupby('User uuid')

# **사용자별**로 정규화 혹은 표준화된 값인지 확인
df['Likes_Normalized_By_User'] = user['Likes'].transform(lambda x: (x - x.min()) / (x.max() - x.min()))
df['Likes_Standardized_By_User'] = user['Likes'].transform(lambda x: (x - x.mean()) / x.std())

# 실제 Likes Score와의 차이 계산
normalized_by_user_difference = np.abs(df['Likes Score'] - df['Likes_Normalized_By_User']).mean()
standardized_by_user_difference = np.abs(df['Likes Score'] - df['Likes_Standardized_By_User']).mean()

print("Likes Score - user-normalized Likes:", normalized_by_user_difference)
print("Likes Score - user-standardized Likes:", standardized_by_user_difference)
```

### 3-2) "Days passed from post"가 큰 이상치 데이터 제거하여 "Year"의 분포를 균일하게 하기

- Q3 + 1.5 * IQR 이상의 데이터 제거하여 "Year" 균일해짐

```
# 1사분위(Q1)와 3사분위(Q3) 계산
Q1 = df['Days passed from post'].quantile(0.25)
Q3 = df['Days passed from post'].quantile(0.75)
IQR = Q3 - Q1
print(Q1, Q3)
# 이상치 기준 계산
lower_bound = Q1 - 1.5 * IQR
upper_bound = Q3 + 1.5 * IQR
print(lower_bound, upper_bound)

df = df[df['Days passed from post'] <= upper_bound]
```
![instagram_year.png](PNG/instagram_year.png)

### 3-3) Day(수치형 데이터)를 Weekday(범주형 데이터)로 변환하기
![instagram_countplot.png](PNG/instagram_countplot.png)
![instagram_weekday.png](PNG/instagram_weekday.png)

## 4. 데이터 변환 및 피처 엔지니어링

### 4-1) hour를 pca를 통해 hour zone으로 나누기

![hour_pca.png](PNG/hour_pca.png)

### 4-2) One-hot encoding 후 correlation 확인

![instagram_heatmap.png](PNG/instagram_heatmap.png)

## 5. 데이터 분할 및 예측
- EDA 전) train: 0.017058693726008767, test: 0.0013833752656855491
- EDA 후) train: 0.6933284436087055, test: 0.6692390909320178

<!-- 김해빈 end -->