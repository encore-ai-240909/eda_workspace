
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


## 6. Key Findings (주요 결과 요약)





<!-- 이예진 end -->






