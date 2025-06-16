# Airbnb K-means Clustering 사례 분석 보고서

- 

## 1. 개요

Airbnb는 전 세계 숙소 데이터를 기반으로 고객에게 더 나은 추천과 맞춤형 서비스를 제공하기 위해 다양한 머신러닝 기법을 사용하고 있습니다. 그 중 K-means Clustering은 숙소를 비슷한 군집으로 나누어 고객의 선호에 맞는 검색 결과를 제공하는 데 활용됩니다. 본 보고서에서는 K-means Clustering을 Airbnb 데이터에 적용해보고, 그 결과와 기대효과를 살펴보겠습니다.

---

## 2. 데이터 설명

이번 분석에서는 Airbnb의 예시 데이터를 사용했습니다. 데이터에는 다음과 같은 주요 컬럼이 포함되어 있습니다:

- `latitude`: 숙소의 위도  
- `longitude`: 숙소의 경도  
- `price`: 숙소의 가격  
- `minimum_nights`: 최소 숙박일수

> **참고:** 실제 Airbnb 데이터는 [Inside Airbnb](http://insideairbnb.com/get-the-data.html)에서 다운로드할 수 있습니다.

---

## 3. 분석 목표

- K-means Clustering을 통해 비슷한 위치와 가격대의 숙소를 그룹화한다.
- 클러스터별 특성을 파악하여 지역별 가격대를 이해한다.
- 클러스터링 결과를 시각화하여 인사이트를 도출한다.

---

## 4. 분석 코드

아래는 Python으로 K-means Clustering을 수행하는 간단한 예시 코드입니다.

```python
# 라이브러리 불러오기
import pandas as pd
from sklearn.cluster import KMeans
import matplotlib.pyplot as plt

# 데이터 불러오기
df = pd.read_csv('airbnb_listings.csv')

# 분석에 사용할 컬럼 선택
X = df[['latitude', 'longitude', 'price']]

# KMeans 모델 학습
kmeans = KMeans(n_clusters=5, random_state=42)
df['cluster'] = kmeans.fit_predict(X)

# 결과 시각화
plt.figure(figsize=(10, 6))
scatter = plt.scatter(df['longitude'], df['latitude'],
                      c=df['cluster'], cmap='viridis', alpha=0.5)
plt.xlabel('Longitude')
plt.ylabel('Latitude')
plt.title('Airbnb Listings Clustering (k=5)')
plt.colorbar(scatter, label='Cluster')
plt.show()
