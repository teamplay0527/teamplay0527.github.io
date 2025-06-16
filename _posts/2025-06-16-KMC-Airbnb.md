# Airbnb K-means Clustering 사례 분석 보고서

- 하임경(limkyoung.ha@lge.com)
- 정한영(hanyoung1.jeong@lge.com)
- 엄정훈(junghoon.um@lge.com)

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
```

## 5. 분석 결과 및 해석

아래는 K-means Clustering으로 Airbnb 숙소 데이터를 군집화한 결과입니다.

![image](https://github.com/user-attachments/assets/37b09696-986d-4033-9570-462b6b1550d9)


> **그림:** K-means 군집화 시각화 예시  
> - 서로 다른 색상은 각각의 클러스터를 나타냅니다.  
> - 지리적으로 인접하고 가격대가 비슷한 숙소들이 하나의 클러스터로 묶였습니다.  
> - 도심과 외곽 지역이 명확히 구분되어 지역별 가격 패턴을 쉽게 파악할 수 있습니다.

**해석:**  
- **도심 지역**은 높은 가격대와 높은 수요로 인해 별도의 군집으로 분류됩니다.  
- **외곽 지역**은 낮은 가격대 숙소가 다수 포함되며, 관광지와 접근성에 따라 군집이 나뉩니다.  
- 이 결과는 Airbnb가 사용자 맞춤형 추천 알고리즘을 개선하고 지역별 가격 전략을 수립하는 데 활용될 수 있습니다.

---

## 6. 기대효과

K-means Clustering 적용을 통해 얻을 수 있는 기대효과는 다음과 같습니다.

- **맞춤형 검색 결과 제공:** 사용자가 원하는 가격대와 선호 지역에 맞춘 검색 필터링 기능 강화
- **수익 극대화:** 지역별 가격대 분석을 통해 가격 정책을 최적화하고 경쟁력을 확보
- **운영 효율화:** 데이터 기반으로 숙소 공급자에게 최적의 가격 및 지역 전략을 제안 가능
- **고객 만족도 향상:** 사용자가 원하는 숙소를 빠르게 찾을 수 있어 플랫폼 이용 경험이 개선됨

---

## 7. 결론

본 분석에서는 Airbnb 숙소 데이터를 활용하여 K-means Clustering을 적용하고 그 결과를 시각적으로 확인했습니다. 그 결과, 지리적 위치와 가격대에 따라 숙소를 효과적으로 군집화할 수 있음을 확인했으며, 이를 통해 사용자 맞춤형 서비스와 가격 전략 수립에 활용할 수 있음을 알 수 있었습니다.

---
