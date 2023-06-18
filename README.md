# Recommending_Books
도서 추천 시스템 모델 (Dacon 제2회 코스포 x 데이콘 도서 추천 알고리즘 AI경진대회 참여)
(https://dacon.io/competitions/official/236093/overview/description)
- 평점 예측 모델 구축 대회
- 제약사항 : 추가 데이터 활용 불가
## 전처리
- User, Item(Book), 출판년도에서 보여지는 값들이 극심하게 차이남
- User-ID, Book-ID, 저자, 출판사는 일반적인 인코딩 수행
- Age는 8세 ~ 80세로 제한
- Location은 일종의 주소로 간주하고 Item2Vec 방식 차용해서 임베딩 수행
- Book-Title은 글자 깨짐, 비영어 언어 등 다른 요소들이 많아 모델 작업에서 제외 (Book-ID와도 중복 가능성)
## 대회 중 (1차 모델링)
- Surprise 라이브러리 사용
- User-ID, Book-ID, 평점을 가지고 행렬분해 알고리즘 수행 (SVD++)
- KNN 같은 기타 모델은 메모리 한계로 수행 X
- Factorisation Machine, DeepFM 등 다른 요소를 반영하는 추천 시스템 모델을 활용하려 했으나 리소스 부족으로 실패
- 그리드 서치 통해서 SVD++ 하이퍼 파라미터 튜닝 모델로 대회 종료
  - n_factors = 2, epochs = 5
  - 대회 결과 RMSE: 3.4376
## 대회 종료 후 (2차 모델링)
- 대회 참여자 대부분이 catboost 알고리즘을 활용하여 모델 구축한 것을 확인
- 사전에 설정한 전처리 방식에 catboost 모델을 사용하여 모델 구축
  - RMSE: 3.2939
- svd++와 catboost 모델을 앙상블 (비율 1:9)
  - RMSE: 3.2933
## 함의 및 개선점
- 추천 시스템이라는 특정 틀에 갖혀 다른 모델을 시도하지 않음
- 리소스 문제(주로 RAM 용량)로 실행할 수 없는 모델들이 많았음
- 다른 추천 시스템 모델 구축하는 방법을 연습해 볼 필요
