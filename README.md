# 역세권 공동주택 실거래정보 데이터 분석
- 서울시립대학교 데이터과학을위한통계방법론(2-2) 과제 정리

## Data Overview
- 데이터명: 역세권 공동주택 실거래 정보
- 제공 기관: 한국부동산원
- 포맷: csv
- 데이터 내용: GIS를 활용하여 역세권(지하철역사로부터 500m 이내) 필지정보를 추출한 후, 해당 정보를 실거래가 공개시스템을 통해 수집한 공동주택 거래정보(매매,전세,월세)와 연계 가공하여 관련 정보를 제공

## Anaysis Overview
- 분석 목적: 매매가, 전세가(보증금), 월세 간 관계를 파악해보기 위함.
- 동대문구 내의 역세권 주택 데이터 전체에 대한 EDA 이후 다세대주택, 오피스텔 데이터를 중심으로 EDA 및 상관분석을 진행함.

## Data
- 주택 유형에 따른 데이터 분포: 아파트(54.3%), 다세대주택(24.3%), 오피스텔(21.5%)
![image](https://github.com/hoorangyee/Stat_for_DS/assets/119475060/47669879-2bec-4020-81c5-7959eca5c07e)

- 2019~2023년 사이에 건축된 건물에 대한 데이터가 많음.
- 대부분의 변수에서 아파트는 넓은 값의 분포를 가짐.
- 대부분의 변수에서 다세대주택, 오피스텔은 특정 값에 집중되어 있는 분포를 보임.
- 대부분의 변수에서 오피스텔은 분포의 꼬리가 매우 짧음.
- 아파트와 다세대주택/오피스텔은 서로 다른 성격의 분포를 보임.
- 특히, 매매가, 전세 보증금, 월세와 같은 가격 데이터에 대해 아파트가 다세대주택/오피스텔보다 높은 값에 더 집중되어 있음.

- 거래 유형에 따른 데이터 분포: 전세(50.7%), 월세(32.5%), 매매(16.7%)
![image](https://github.com/hoorangyee/Stat_for_DS/assets/119475060/df8eeb98-d3d2-422a-a208-8c92e386d9cf)

- 거래 유형에 따라 데이를 나눈 뒤, 전용면적 당 가격 변수를 추가함.
- 거래 유형에 따라 각 변수의 분포를 확인해보았을 때, 앞서 확인했던 다세대주택/오피스텔의 분포와 크게 다르지 않음.
- 전용면적 당 가격 변수는 매매 데이터에서 하위 40% 정도에 분포가 집중되어 있는 반면, 전세/월세 데이터에서는 종모양의 분포를 보임.

## Correlation Anaysis
### 거래 유형: 매매
![image](https://github.com/hoorangyee/Stat_for_DS/assets/119475060/27d6ae11-23aa-46ee-9179-ee60bf6f567c)

- 매매가는 전용면적과 강한 양의 상관관계, 층수와 음의 상관관계가 있음.
- 전용면적 당 매매가는 건축년도와 강한 양의 상관관계가 있음.

### 거래 유형: 전세
![image](https://github.com/hoorangyee/Stat_for_DS/assets/119475060/83012f58-719c-4b97-980f-0c90a688665d)

- 전세 보증금은 건축년도, 전용면적과 양의 상관관계가 있음.
- 전용면적 당 전세 보증금은 건축년도와 강한 양의 상관관계, 전용면적과 음의 상관관계가 있음.

### 거래 유형: 월세
![image](https://github.com/hoorangyee/Stat_for_DS/assets/119475060/41a1c0e3-153c-4184-a353-1deafef3fd24)

- 월세와 전용면적 당 월세 사이에 강한 양의 상관관계가 있음.
- 전용면적당 월세는 건축년도와 양의 상관관계, 보증금과 음의 상관관계가 있음.
- 월세와 보증금 사이에 음의 상관관계가 있음.

## Linear Regression
### 거래 유형: 매매
![image](https://github.com/hoorangyee/Stat_for_DS/assets/119475060/1d888973-340c-4264-a13b-ba45c500f0cc)

coef: [[24.21015714]], intercept: [-47917.00715251]

### 거래 유형: 전세
![image](https://github.com/hoorangyee/Stat_for_DS/assets/119475060/50d2402d-df2f-4735-ba76-0771ecb12cb6)

coef: [[23.26837929]], intercept: [-46147.83108728]

### 거래 유형: 월세
![image](https://github.com/hoorangyee/Stat_for_DS/assets/119475060/f264a504-4b7b-44df-bfe1-0ab8ec320f63)

coef: [[0.09015274]], intercept: [-178.80465679]

![image](https://github.com/hoorangyee/Stat_for_DS/assets/119475060/940ae3a0-3ef5-4390-a705-081b932765eb)

coef: [[0.03115278]], intercept: [0.7650987]

## Spline Regression
### 거래 유형: 매매
![image](https://github.com/hoorangyee/Stat_for_DS/assets/119475060/ee96599d-df18-4df7-afab-2317d2ceffea)

min or max point: [161.12222222 331.7]

### 거래 유형: 전세
![image](https://github.com/hoorangyee/Stat_for_DS/assets/119475060/809ffb73-8907-40f7-b22d-f0d4afac8e80)

min or max point: [141.18787879 262.20606061 383.22424242]

### 거래 유형: 월세
![image](https://github.com/hoorangyee/Stat_for_DS/assets/119475060/e5ce5755-a4bf-4ddb-bb98-f5419dda1190)

mix or max point: [126.50707071 199.49191919 340.5959596 ]

## Conclusion
- 아파트와 다세대주택/오피스텔은 다른 분포를 띰.

- 아파트는 넓은 분포, 다세대주택/오피스텔은 집중된 분포를 띰.
  
- 전용면적당 매매가, 전용면적당 전세보증금, 전용면적당 월세와 건축년도 사이에는 모두 양의 상관관계가 있음. 

- 건축년도가 전용면적당 가격에 주요한 영향을 끼침.

- 전용면적당 전세보증금에 대해서는, 전용면적 변수도 어느정도 유의미한 영향이 있는 것으로 보임.

- 인근역과 일정 거리 이내로 가까운 경우(약 140m ~ 320m까지) 전용면적당 가격이 감소하고, 그 이후부터 다시 가격이 증가하는 양상을 보임.

- 이는 지하철역 인근은 소음, 혼잡 문제가 있기 때문에 일정 거리까지는 가격에 부정적인 영향을 미치고, 적정 거리 이상부터는 지하철역에 대한 접근성의 영향이 더 커져 가격이 올라가는 것으로 보임.

## Discussion

- 이번 분석에서는 역세권 공동주택 데이터를 주택 유형에 따라 나누어 EDA를 수행한 후, 다세대주택/오피스텔 데이터에 대해 상관분석 및 선형회귀분석, 스플라인 회귀 분석을 수행하였음.
  
- 분석 결과, 전용면적당 건물 가격(매매가, 전세 보증금, 월세)은 건축년도에 큰 영향을 받는 것으로 나타났음.
  
- 선행 연구들에서 언급된 역까지의 거리와 건물 가격 사이의 음의 이차함수 형태의 관계도 어느 정도 확인할 수 있었으나, 스플라인 회귀 분석 결과는 통계적으로 완전히 유의미하지 않았음.
  
- 이번 분석에서는 선행 연구들처럼 역을 지상역과 지하역으로 구분하거나 역의 기능별로 다르게 분석하지 않았기 때문에, 다른 결과가 나왔을 수 있음.
  
- 이번 분석을 통해 역세권 공동주택의 전용면적당 건물 가격에 영향을 미치는 요인들을 확인하고, 인근역까지의 거리와 전용면적당 건물 가격 사이의 관계를 파악하였음.
  
- 이러한 분석은 향후 역세권 개발의 참고 자료로 활용될 가치가 있음. 추후 연구에서는 역을 더 세밀하게 구분하여 분석함으로써 더 많은 유의미한 결과를 도출할 수 있을 것으로 기대됨.










