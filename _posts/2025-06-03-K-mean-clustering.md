[PDF 보기](/files/K-평균 군집화_하임경_정한영_엄정훈.pdf)

추천주제 : K-Mean Clustering : 역사, 원리, 실용 사례

- **하임경**(limkyoung.ha@lge.com)  
- **정한영**(hanyoung1.jeoung@lge.com)  
- **엄정훈**(junghoon.um@lge.com)  

---
주제선정이유 : 비지도 학습 중 가장 많이 쓰이는 알고리즘 중 하나, 개념이 단순해 설명하기 좋음.
- 장점 : 그래프와 시각적 예시가 풍부, 다양한 데이터에 쉽게 적용.
- 활용사례 : 고객 세분화, 이미지 압축, 이상 탐지 등.

---
Category
1. K-Mean Clustering의 역사
2. K-Mean Clustering의 원리
3. 실용 사례 예시

---   


1. K-Mean Clustering의 역사

K-Mean Clustering의 개념은 1950년대 중반에 처음 등장했다. 1967년 제임스 맥퀸(James MacQueen)이 “K-평균”이라는
명칭을 사용했지만, 그 아이디어는 1956년 폴란드 수학자 후고 스타인하우스(Hugo Steinhaus)가 처음 제안했다
. 이후 벨 연구소의 미국 물리학자 스튜어트 로이드(Stuart Lloyd)는 1957년에 해당 아이디어를 확장하여 실제
알고리즘을 고안했으나, 이 내용은 1982년에야 논문으로 출판되었다 . 1965년에는 미국 통계학자 에드워드 포
기(Edward W. Forgy)도 유사한 방법을 발표하여, 이 알고리즘은 때때로 ‘로이드-포기 알고리즘’으로도 불린다 . 
폴란드의 수학자 후고 스타인하우스(1887–1972). 그는 1956년 군집화 개념을 제안하여 K-평균 알고리즘의 기초를 마
련했다 . 이외에도 벨 연구소의 스튜어트 로이드(1957년 제안), 미국 통계학자 에드워드 포기(1965년 발표), 그리고
제임스 맥퀸(1967년 “K-평균” 명칭 사용) 등이 이 알고리즘의 발전에 중요한 기여를 했다.

---

2. K-Mean Clustering의 원리

(1) 정의  
K-평균은 데이터를 **K개의 그룹(클러스터)**로 나누어, 각 그룹 내 유사한 특성을 가진 데이터끼리 묶는 **비지도 학습** 알고리즘입니다.

---

(2) 알고리즘 단계별 설명

① 초기 중심 설정 (Initialization)

- 임의로 K개의 중심점을 선택합니다.

② 군집 할당 (Assignment)

- 각 데이터 포인트를 가장 가까운 중심점에 할당합니다.  
- 주로 **유클리디안 거리**를 사용합니다.

③ 중심 재계산 (Update)

- 클러스터 내 데이터의 평균 위치로 중심점을 이동시킵니다.


④ 반복 및 수렴 (Convergence)

- 중심점이 더 이상 변하지 않을 때까지 2~3단계를 반복합니다.

---

(3) 알고리즘 흐름

초기 중심 설정 → 클러스터 할당 → 중심 재계산 → 중심 변화 확인 → 반복 or 종료

---

3. 실용 사례 예시

(1) 대표 사례: 고객 세분화

기업들은 고객의 나이, 소득, 구매 이력 등 특성 데이터를 K-평균으로 군집
화하여 비슷한 성향의 고객 그룹을 식별한다 . 이를 통해 각 그룹(예: 고소득층, 저소득 중간 사용층, VIP 고객 등)에
맞는 맞춤형 마케팅 전략을 수립할 수 있다. 예를 들어, 연구에 따르면 K-평균은 비지도 학습을 이용해 고객 하위 집단을
자동으로 찾아내고, 이를 통해 마케팅 타겟팅 효율을 높일 수 있음을 보여준다.

---

(2) 아이리스(Iris) 데이터셋 분석

아이리스 데이터셋은 1936년 로널드 피셔가 소개한 대표적인 다변량 데이터로, 붓꽃 세 종(세
토사·버지니카·버시컬러) 각 50개씩, 총 150개 샘플에 대해 꽃받침 길이/너비와 꽃잎 길이/너비 등 4개 특성이 측정되어
있다 . K-평균을 이용해 이 데이터를 으로 군집화하면, 아래 그림처럼 실제 종 분류와 유사한 패턴으로
데이터가 나뉘는 것을 볼 수 있다. 즉, K-평균은 비지도학습임에도 불구하고 종(Setosa 등)에 따른 클러스터를 대체로
잘 찾아낸다.
아이리스 데이터셋의 K-평균 군집화 예시: 3차원 산점도에서 3개의 클러스터(k=3)를 그린 결과(각 색은 서로 다른 클러
스터) . 왼쪽 위는 클러스터 수 일 때, 오른쪽 위는 일 때 결과이며, 오른쪽 아래는 실제 정답(붓꽃 종)을 나타낸다. 인 경우 K-평균 결과가 실제 종 분포와 비교적 유사함을 알 수 있다.

---

(3) 최신 기업 사례

최근에는 실무에서도 K-평균 군집화가 널리 활용된다. 예를 들어, Airbnb 기술팀은 호스트의 숙소 이용
가능 패턴 데이터를 기반으로 K-평균을 적용하여 8개의 유형으로 호스트를 세분화했다 . 이들은 값을 2에서 10까
지 테스트한 후 엘보우 기법을 이용하여 이 최적임을 판단했으며 , 각 클러스터를 이용해 호스트 맞춤형 지원
서비스를 제공하고 있다. 유사하게, 우버(Uber)는 뉴욕시 차량 픽업 위치 데이터를 K-평균으로 클러스터링하여 픽업 허
브(clusters centroid)를 찾았다 . 이를 통해 운전자에게 특정 중심 지역 주변에서 대기하도록 안내하여 승객 대기
시간을 최소화했으며, 수요·공급 비율에 따라 동적인 요금 책정(서지 프라이싱)에도 활용하고 있다 . 이러한 사례들
은 K-평균을 통해 복잡한 실세계 데이터를 효과적으로 분할하여 비즈니스 문제(마케팅 전략, 운영 최적화 등)를 해결한
예들이다


---

※ 참고자료

K-평균 군집화의 개념과 역사 , 알고리즘 원리 , 실용사례 등을 참고하였다.  
k-means clustering - Wikipedia  
[https://en.wikipedia.org/wiki/K-means_clustering](https://en.wikipedia.org/wiki/K-means_clustering)  
K-Means Clustering for Machine Learning Explained  
[https://www.deeplearning.ai/the-batch/k-means-clustering-group-think/](https://www.deeplearning.ai/the-batch/k-means-clustering-group-think/)  
K-Means Clustering Explained  
[https://neptune.ai/blog/k-means-clustering](https://neptune.ai/blog/k-means-clustering)  
Customer Segmentation using KMeans in R | GeeksforGeeks  
[https://www.geeksforgeeks.org/customer-segmentation-using-kmeans-in-r/](https://www.geeksforgeeks.org/customer-segmentation-using-kmeans-in-r/)  
Iris flower data set - Wikipedia  
[https://en.wikipedia.org/wiki/Iris_flower_data_set](https://en.wikipedia.org/wiki/Iris_flower_data_set)  
From Data to Insights: Segmenting Airbnb’s Supply | by Alexandre Salama | The Airbnb Tech Blog | Medium  
[https://medium.com/airbnb-engineering/from-data-to-insights-segmenting-airbnbs-supply-c88aa2bb9399](https://medium.com/airbnb-engineering/from-data-to-insights-segmenting-airbnbs-supply-c88aa2bb9399)  
Uber trip segmentation using K-means clustering  
[https://www.linkedin.com/pulse/uber-trip-segmentation-using-k-means-clustering-khatre-csm-pmp](https://www.linkedin.com/pulse/uber-trip-segmentation-using-k-means-clustering-khatre-csm-pmp)  
