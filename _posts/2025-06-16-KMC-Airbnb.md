# 🏠 Airbnb 고객 세분화를 위한 K-Means Clustering 프로젝트

---

## 📌 1. 개요

Airbnb는 다양한 사용자 데이터를 보유하고 있으며, 고객의 행동 패턴을 이해하고 맞춤형 서비스를 제공하기 위해  
**K-Means Clustering** 기법을 활용하여 사용자군을 세분화했습니다.

본 프로젝트는 Airbnb 사례를 바탕으로 K-Means Clustering을 적용한 고객 세분화 프로세스를 실습 형태로 재현합니다.

---

## 📂 2. 데이터 설명

| 변수명 | 설명 |
|--------|------|
| `booking_freq` | 연간 예약 빈도 |
| `stay_duration` | 평균 숙박 일수 |
| `room_type` | 숙소 타입 (0: 개인실, 1: 집 전체) |
| `city_center_preference` | 도심 선호도 (0 ~ 1) |

> ⚙️ **데이터는 가상의 샘플 데이터이며, 실제 Airbnb의 데이터 구조를 모방했습니다.**

---

## 🎯 3. 분석 목표

✅ 사용자 행동 기반으로 유사한 고객 그룹 도출  
✅ 그룹별 주요 특성을 파악  
✅ 맞춤형 마케팅 및 추천 서비스 아이디어 제시  
✅ 데이터 기반 의사결정에 활용

---

## 💻 4. 분석 코드

아래는 Python(scikit-learn)으로 작성된 K-Means Clustering 분석 코드입니다.  
전체 코드는 `airbnb_kmeans.ipynb` 파일로 제공됩니다.

```python
# 필요한 라이브러리 설치
# pip install numpy pandas scikit-learn matplotlib seaborn

import numpy as np
import pandas as pd
from sklearn.cluster import KMeans
from sklearn.preprocessing import StandardScaler
import matplotlib.pyplot as plt
import seaborn as sns

# --------------------------------
# 1) 가상 사용자 데이터 생성
# --------------------------------
np.random.seed(42)
n_users = 500

data = pd.DataFrame({
    'booking_freq': np.random.poisson(3, n_users),
    'stay_duration': np.random.normal(5, 2, n_users),
    'room_type': np.random.choice([0, 1], n_users),
    'city_center_preference': np.random.uniform(0, 1, n_users)
})

# --------------------------------
# 2) 표준화
# --------------------------------
scaler = StandardScaler()
X_scaled = scaler.fit_transform(data)

# --------------------------------
# 3) Elbow Method로 최적 K 찾기
# --------------------------------
inertia = []
K = range(1, 10)
for k in K:
    kmeans = KMeans(n_clusters=k, random_state=42)
    kmeans.fit(X_scaled)
    inertia.append(kmeans.inertia_)

plt.figure(figsize=(8, 5))
plt.plot(K, inertia, 'bo-')
plt.xlabel('Number of Clusters (K)')
plt.ylabel('Inertia')
plt.title('Elbow Method for Optimal K')
plt.grid(True)
plt.savefig('images/elbow_method.png')
plt.show()

# --------------------------------
# 4) K-Means 학습 및 군집화
# --------------------------------
kmeans = KMeans(n_clusters=3, random_state=42)
data['cluster'] = kmeans.fit_predict(X_scaled)

# --------------------------------
# 5) 군집별 통계 확인
# --------------------------------
print(data.groupby('cluster').mean())

# --------------------------------
# 6) 군집 시각화
# --------------------------------
sns.scatterplot(
    x='booking_freq',
    y='stay_duration',
    hue='cluster',
    palette='Set2',
    data=data
)
plt.title('Airbnb Customer Segmentation')
plt.xlabel('Booking Frequency')
plt.ylabel('Stay Duration')
plt.savefig('images/clusters.png')
plt.show()

#5. 분석 결과 및 해석
# Elbow Method 결과

K=3에서 관성이 급격히 완화되므로, 3개의 고객군으로 분류하는 것이 적절하다고 판단됩니다.

# 군집 시각화 결과

클러스터별로 예약 빈도, 숙박 기간이 명확히 구분됨

예:

Cluster 0: 예약 빈도 낮음, 숙박 기간 짧음 → 단기 출장형

Cluster 1: 예약 빈도 높음, 숙박 기간 길음 → 장기 여행자/디지털 노마드형

Cluster 2: 평균적 사용자군

# 군집별 특성 요약
클러스터	예약 빈도	평균 숙박 일수	숙소 타입	도심 선호도
0	낮음	짧음	개인실 비율 높음	도심 선호
1	높음	김	집 전체 선호	도심 선호 낮음
2	중간	중간	혼합	평균적 선호

# 6. 기대 효과
# 맞춤형 마케팅
→ 가족 여행자군에는 가족 전용 숙소 추천, 단기 출장군에는 비즈니스 숙소 제공

# 추천 알고리즘 고도화
→ 유사 사용자군의 인기 숙소를 추천

# 신규 서비스 개발
→ 장기 숙박 고객을 위한 체험 프로그램 설계

# 이탈 방지 전략 수립
→ 예약 횟수가 줄어드는 사용자군에 할인 쿠폰 제공

# 7. 결과 보고서
Airbnb는 K-Means Clustering으로 고객을 행동 기반으로 세분화하여,

고객 맞춤형 서비스를 제공하고,

마케팅 ROI를 높이고,

플랫폼 사용자 만족도를 향상시켰습니다.

본 실습 프로젝트는 K-Means Clustering의 강력한 활용 가능성을 실제 비즈니스 사례에 맞춰 확인할 수 있는 좋은 예시가 됩니다.
