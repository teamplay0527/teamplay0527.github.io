#  Airbnb 고객 세분화를 위한 K-Means Clustering

---

##  1. 개요

Airbnb는 다양한 사용자 데이터를 보유하고 있으며, 고객의 행동 패턴을 이해하고 맞춤형 서비스를 제공하기 위해  
**K-Means Clustering** 기법을 활용하여 사용자군을 세분화했습니다.

본 프로젝트는 Airbnb 사례를 바탕으로 K-Means Clustering을 적용한 고객 세분화 프로세스를 실습 형태로 재현합니다.

---

##  2. 데이터 설명

| 변수명 | 설명 |
|--------|------|
| `booking_freq` | 연간 예약 빈도 |
| `stay_duration` | 평균 숙박 일수 |
| `room_type` | 숙소 타입 (0: 개인실, 1: 집 전체) |
| `city_center_preference` | 도심 선호도 (0 ~ 1) |

---

##  3. 분석 목표

✅ 사용자 행동 기반으로 유사한 고객 그룹 도출  
✅ 그룹별 주요 특성을 파악  
✅ 맞춤형 마케팅 및 추천 서비스 아이디어 제시  
✅ 데이터 기반 의사결정에 활용

---

##  4. 분석 코드

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
```


# Airbnb 고객 세분화 분석 결과 및 해석

##  Elbow Method 결과

![Elbow Method](images/elbow_method.png)

- Elbow Method 그래프에서 K=3에서부터 관성 감소가 완만해지는 지점이 나타납니다.  
  ➡️ **최적 군집 수 K=3**으로 판단.

---

##  군집별 분포 시각화

![Customer Clusters](images/clusters.png)

- 위 시각화는 예약 빈도(`booking_freq`)와 평균 숙박 일수(`stay_duration`)를 기준으로 고객을 3개 군집으로 나눈 결과입니다.
- 색상은 각각 다른 클러스터를 나타내며, 다음과 같은 해석이 가능합니다:

| 클러스터 | 특징 | 해석 |
|----------|------|------|
| Cluster 0 | 예약 빈도 낮음, 숙박 일수 짧음 | 단기 출장자, 도심 근처 선호 |
| Cluster 1 | 예약 빈도 높음, 숙박 일수 김 | 장기 체류자 (디지털 노마드 등), 도심 외곽 선호 |
| Cluster 2 | 중간 수준의 예약 및 숙박 | 평균적인 일반 사용자군 |

---

## 기대 효과

### 1. 맞춤형 마케팅

- **Cluster 0** → 비즈니스 전용 숙소 추천, 빠른 체크인 기능 제공  
- **Cluster 1** → 장기 숙박자 할인, 지역 체험 프로그램 제안  
- **Cluster 2** → 일반적인 사용자 대상 다채로운 캠페인 설계

---

### 2. 추천 알고리즘 고도화

- 각 클러스터에서 인기가 많은 숙소, 지역, 호스트 특성을 **동일 클러스터 사용자에게 추천**

---

### 3. 신규 서비스 기획

- **Cluster 1** 대상: 장기 체류자를 위한 코워킹 옵션, 주간 청소 서비스, 지역 커뮤니티 소개 등  
- 사용자 니즈 기반의 **맞춤형 부가 서비스** 도출 가능

---

### 4.  이탈 방지 전략

- 최근 3개월간 예약 빈도 하락 중인 사용자 클러스터 감지 → **타겟 프로모션, 리마인드 이메일** 전송  
- 체류 유형에 따른 **UX 개선** 전략 설계

---

##  최종 결과 요약

Airbnb는 K-Means Clustering 기반의 고객 세분화를 통해 다음을 달성했습니다:

- ✔️ 고객 니즈에 맞는 숙소 추천
- ✔️ 마케팅 예산 효율화
- ✔️ 서비스 개인화 전략 도입
- ✔️ 고객 이탈 감소 및 경험 개선
