# 🙈 K3J1 EDA 보고서 🙉

## <데이터 보고서>

### 👨‍👩‍👧‍👦 팀원소개

- 3명의 김씨(K3)와 1명의 조씨(J1)로 구성된 K3J1
- 김정아, 김진수, 김희애, 조은비

### 1. 서론
인도는 한 나라의 다양한 요소가 공존하고 있습니다. 힌디어 카나다어, 타밀어 , 텔루구어를 비롯한 22개 언어가 공용어로 지정돼 있으며 이외에도 1600개의 언어가 존재하는 것으로 추정됩니다. 또한 힌두교, 이슬람, 기독교, 시크교 등 여러 종교가 공존하고 있습니다.
이처럼 다인종, 다언어, 다종교, 다문화 국가에 사는 인도 사람들은 다양한 소피패턴을 갖고 있을거라고 예상하고고 인도사람들의 소비패턴에 대한 데이터를 선정하게 되었습니다.

#### 목적: EDA의 목적과 데이터 분석의 배경 설명.

#### 데이터셋 설명
**Indian Personal Finance and Spending Habits**
- 출처 : kaggle의 데이터 (https://www.kaggle.com/datasets/shriyashjagtap/indian-personal-finance-and-spending-habits/code)
- 변수
  [Personal Data]
  - Income: 월 소득
  - Age: 나이
  - Dependents: (부양가족)
  - Occupation: 직업 유형 또는 고용 형태
  - City_Tier: 거주 지역
      city_tier1 =  대도시
      city_tier2 = 신도시
      city_tier3 = 교외
  
  [Spendings] 
  - Rent : 집세, 방세, 임차료
  - Loan_Repayment : 대출상환
  - Insurance : 보험
  - Groceries : 식료품
  - Transport : 교통
  - Eating_Out : 외식
  - Entertainment : 오락
  - Utilities :공과금
  - Healthcare : 건강관리
  - Education : 교육
  - Miscellaneous : 그 외

  [Financial Goals & Savings]
  - Desired_Savings_Percentage : 희망 저축 비율
  - Desired_Savings : 희망 저축 금액
  - Disposable_Income : 가처분 소득 (Income - all spendings)

  [Potential Savings]
  - Potential_Savings_Groceries : 식료품 지출에 대한 잠재적 절감액
  - Potential_Savings_Transport : 교통비에 대한 잠재적 절감액
  - Potential_Savings_Eating_Out : 외식비에 대한 잠재적 절감액
  - Potential_Savings_Entertainment : 오락 지출에 대한 잠재적 절감액
  - Potential_Savings_Utilities : 공과금에 대한 잠재적 절감액
  - Potential_Savings_Healthcare : 건강관리 지출에 대한 잠재적 절감액
  - Potential _Savings_Education : 교육비에 대한 잠재적 절감액
  - Potential_Savings_Miscellaneous. 그 외 지출에 대한 잠재적 절감액


#### 결측치 분석
- 결측치 없음.(*결측치: 데이터셋에서 특정 값이 누락된 상태를 의미)


### 3. 기초 통계량
- 변수별 평균, 중앙값, 분산, 표준편차
  <br>
![스크린샷 2024-10-28 112245](https://github.com/user-attachments/assets/3f08a628-913b-46fc-b331-9ca66700b83b)
![스크린샷 2024-10-28 112255](https://github.com/user-attachments/assets/626b70d9-88f7-40dc-8802-0cfc2fc52d5a)
![스크린샷 2024-10-28 112303](https://github.com/user-attachments/assets/8277537b-9a66-40a7-a974-c40ce0b56bab)
![스크린샷 2024-10-28 112309](https://github.com/user-attachments/assets/4d87c6d4-5551-4cfc-977a-bcac015d3f70)

- 나이별, 부양가족별, 직업별 분포

![image](https://github.com/user-attachments/assets/7df25ceb-5ed7-464a-83b7-c67441625381)
![image](https://github.com/user-attachments/assets/42f73b63-521a-47dd-b125-cfc6253b8951)
![image](https://github.com/user-attachments/assets/6fcc6519-64cd-4996-bc3f-1257bf486cab)


### 4. 변수 간 관계

#### 상관 분석

- 변수 간 상관계수 계산 및 시각화 (히트맵 등).
- 산점도: 주요 변수 간의 관계를 나타내는 산점도 시각화.

### 5. 시각화

- 그래프 및 차트: 데이터의 인사이트를 명확히 전달하기 위한 다양한 그래프(막대그래프, 파이차트, 선그래프 등).
- 해석: 각 시각화에 대한 설명과 해석.

### 6. 인사이트 및 결론

#### 주요 발견

- 예시) 수입이 많을수록 지출도 함께 증가함. (수입 ↑ = 지출 ↑)

#### 후속 조치

- 다음 단계(예: 추가 분석, 모델링)와 관련된 제안.

---



## 나이에 따른 수입 변화
<br>

![image](https://github.com/user-attachments/assets/1f45c97f-f144-4e08-8457-6cc40a5a9de3)

<br>
나이가 많을수록 전체적인 수입이 감소하는 추세인 걸 알 수 있습니다. 여기서 더 두드러지는 것은 10-50대까지는 비교적 완만한 곡선으로 감소하는 반면 60대 이상부터는 급격하게 수입이 감소되는 것을 알 수 있습니다.
<br>

## 나이에 따른 Loan repayment
<br>
10대부터 60대까지 세대에 따른 income 대비 loan repayment에 대하여 아래의 그래프에 나타내었습니다. 
10대에서 가장 높은 loan payment 비율을 보여주고 있으며 이는 학자금 대출에 의한 loan payement라고 생각되며 20대부터 50대까지는 유사한 비율을 보이고 있습니다.
60대에서 다시 상대적으로 높은 비율을 보이고 있습니다.

<img src="./data/Loan_repayment_gen_tier.png" width = '400px'>

![image](https://github.com/user-attachments/assets/7bcc3587-af58-4a60-a3c0-1df063a17495)



## 지역에 따른 Income 및 Rent가 Income에서 차지하는 비율
<br>
인도는 기반 산업 및 지형학적 특성 등으로 인하여 Tier1,2,3의 카테고리로 나뉘며 Tier1는 가장 발달된 도시를 의미하며 최근 인도 국가 정책으로 인하여 Tier2,3 도시들에 대한 투자 및 
기업체 유치등의 활발한 투자가 이루워지고 있습니다. 따라서 다양한 대기업들이 Tier2,3 지역에 분포해 있으며 아래 그래프와 같이 Tier 2,3의 평균 Income이 상대적으로
높음을 보여주고 있습니다. 하지만 전통적인 대도시로 인하여 Tier1이 Income대비 높은 rent를 보이고 있으며 Tier 3 에서 가장 낮은 비율을 보이고 있습니다.

<img src="./data/tier_income.png" width = '400px'>

<img src="./data/percent_rent.png" width = '400px'>



## 소득 범위에 따른 지출 내역
<br>
소득을 5개 범위로 나누고, 이에 따른 지출을 누적 그래프로 살펴봤습니다. 소득 범위는 ['Income'].describe()를 했을 때 나오는 min, 25%, 50%, 75%, max 값을 기준으로 구분했습니다. 

단순히 비율로만 따졌을 때는 소득 범위와 관계 없이 지출 내역이 거의 비슷하게 나타나지만, 절대 평균 지출값을 시각화하여 소득 범위별 차이를 살펴보면 소득이 높을수록 지출의 절대값이 증가하는 것이 더 확실하게 나타납니다.
<br>
![](https://github.com/encore-ai-240909/eda_workspace/blob/master/K3J1/data/Income_Range_Expend_Categories.png?raw=true)
![](https://github.com/encore-ai-240909/eda_workspace/blob/master/K3J1/data/Income_Range_Expend_Categories_2.png?raw=true)



## 각 소비 항목에 대한 실제 지출량 및 Potential Savings 비교
<br>
  다음은 각 소비 항목에 대한 실제 지출 및 potential savings에 대한 비교입니다. 각 항목에 대한 분포 이해 및 비교를 위하여 scatter plot을 사용하였으며 
추가적으로는 분포에 대한 linear regression을 그래프에 같이 나타내어 전체적인 추세를 볼수있도록 하였습니다. 좌측 상단에는 linear regression에 대한 slope 및 intercept를 나타내었고
slope는 각 항목이 증가함에 따른 potential savings를 나타내는 비율로 slope가 클수록 비용 절감의 가능성이 높다는 것을 의미합니다.

  여러 Potential savings data 대부분은 아래 나타낸 Eating_out, Groceries 와 같이 실제 소비가 증가함에 따라서 약 17~18 %의 비율로 savings가 늘어남을 보이고 있습니다.
하지만 Education과 Healthcare 항목은 상대적으로 낮은 slope(약 3 %)를 보였습니다. 이는 인도 사회에서 교육 및 건강에 대한 지출이 늘어나더라도 잠재적으로 지출을 줄일 수 있는 부분이 적다는 것을 의미하며 
또한, 교육열 및 건강에 대한 관심이 높다는 것을 의미합니다. 


<br>
<img src="./data/Poten_saving_Eatingout.png" width = '200px'> <img src="./data/poten_saving_Groceries.png" width = '200px'>
<img src="./data/poten_savings_Edu.png" width = '200px'> <img src="./data/poten_savings_health.png" width = '200px'>

<br>
이러한 경향은 아래의 heatmap에서도 잘 드러나고 있음을 알 수 있습니다. Heatmap plot은 각 변수간의 상관관계를 나타내는 plot으로 1에 가까울수록 두 변수가 비례하는 관계를
보이고 -1에 가까울수록 반비례임을 나타냅니다. Potential savings education의 경우, 약 0.5에 근접한 수치를 보이며 상대적으로 다른 변수에 비하여 낮은 수치를 보이고 있습니다.
이는 education 분야에서 소비를 줄일수 있는 가능성이 낮다고 볼 수 있습니다. 

![output_fi](https://github.com/user-attachments/assets/733d781c-24e2-45d5-9b47-363e407ff10b)
<br>
## 교육비, 건강관리 지출
<br>

![image](https://github.com/user-attachments/assets/156be67f-cb08-47f6-ada4-0c0970387172)

<br>
나이가 많을수록 education 지출이 줄고, healthcare 관련 지출이 늘어날 것이라고 예상한 것과 달리 비교적 완만한 형태의 그래프가 나왔습니니다. 이는 앞서 말한 결과와 같은 맥락으로 education, healthcare대한 지출을 줄일 가능성이 낮다고 볼 수 있습니다.

<br>

## 가처분 소득에 대한 희망 저축금액 비율
<br>

![image](https://github.com/user-attachments/assets/3da5daab-e299-4de5-949f-6043594a51ca)
![image](https://github.com/user-attachments/assets/03c194cb-43b2-4a5b-949e-b1661b49da73)

<br>
그래프를 통해 가처분 소득이 늘어날수록 희망 저축금액은 증가한다는 것을 알 수 있습니다. 이 때 가처분 소득에 따른 희망 저축금액이 중상위층까지는 완만하게 증가하지만 상위층에 급격하게 증가하다는 것을 알 수 있습니다. 
