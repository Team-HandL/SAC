# 프로젝트 목표 📌

예술의전당 콘서트홀 공연·예매 데이터 분석을 통한 공연 특성별 좌석 그룹화

1. 장소는 ‘예술의전당 콘서트홀’로 한정
2. ‘유료’ 티켓 예매 데이터를 활용
3. 전체 좌석 등급은 ‘R석, S석, A석, B석, C석’ 5등급으로 지정
4. 공연별 특성을 분석하여 군집화를 수행하고, 각 군집별 좌석 등급 분포 특성 파악

# 데이터 전처리 📌

[데이터 전처리 로직](https://github.com/Team-HandL/SAC/blob/main/basic.ipynb)

## Feature 가공

- 날짜 데이터 형식/타입 통일 및 요일 추출
- 좌석과 할인 정보 구분 및 이진화가 가능한 Feature 가공

## 파생변수 생성

- 멤버십 등급 : 6개 column으로 나뉘어 결측이 매우 많았던 멤버십 정보를무료/유료의 2개 column으로 통합하여 결측을 제거
- 좌석 선호도 : 좌석 예매 시각에 따른 선호도를 나타내는 Feature 생성
- 공연ID : 기존 공연 id의 중복성을 해결하기 위해 공연 장소와 시간을 기준으로  새로운 index를 정의하여 id를 생성
- 티켓 원가, 좌석 등급 : 할인율, 최종판매가를 활용해 원가 산정 후, 공연별 좌석 등급 생성

## 결측치 처리

[결측치 처리를 위한 가설 검정](https://github.com/Team-HandL/SAC/blob/main/EDA.ipynb)

나이 데이터의 결측치 처리를 위해 나이와 유료/무료 멤버십의  가설 수립 및 확인
- 각 셀의 기대빈도>5, 두 변수는 범주형 변수이므로 카이제곱검정으로 두 변수 간의 연관성 측정

<p align='center'><img src="https://github.com/Team-HandL/SAC/assets/77615059/e54fa56f-36e3-4e9e-b164-006ff13451f5" height=250></p>

# K-means Clustering 📌

[clustering 실험 코드](https://github.com/Team-HandL/SAC/blob/main/02_ML_Modeling.ipynb)

[군집별 피쳐 시각화](https://github.com/Team-HandL/SAC/blob/main/03_Data_Analysis.ipynb)

1. **vanilla :** k = 2 ~ 13으로 변화시키며 실루엣 계수 측정
2. **PCA 적용** : 7개의 주성분으로 전체 분산의 89%를 설명
3. **OLS** **Regression Stepwise :** 제거 결과 4개의 변수가 남았으나 R-squared = 0.21로 낮은 설명력

- 세 모델 모두 최적의 k=7이나, 모델 3의 설명력이 낮고, 모델 2의 경우 선택된 변수들만으로는 해석의 어려움이 존재
- 따라서 k=7로 군집화를 수행하되, 원래의 변수들을 포함하여 시각화를 통해 군집별 특성을 하나씩 직접 확인

# 군집별 좌석 등급 시각화 📌

[heatmap 시각화](https://github.com/Team-HandL/SAC/blob/main/05_Cluster_Visualization.ipynb)

- Pivot table, Heatmap 활용 : 전체 좌석 정보를 기반으로 7개의 군집별 좌석 등급(R석, S석, A석, B석, C석) 최종 시각화
<p align='center'><img src="https://github.com/Team-HandL/SAC/assets/77615059/eadb5233-374e-4cbc-8259-b40dba8488dc" height=150></p>

# 프로젝트 회고 📌

- 필요 데이터, 방법과 해석이 명확히 이루어지기 위한 문제 정의의 중요성을 배움
- 통계적 가설검정을 활용한 결측값 처리를 시도해보는 과정이 유의미했음
- 좌석 분포 시각화를 Heatmap으로 접근해보는 과정이 흥미로웠음
- 데이터 분석가 관점에서의 DB 설계에 대해 생각해볼 수 있었음
