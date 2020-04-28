## Acron_Final_Project
영화정보를 통한 흥행 예측


관람객 평점 을 통한 감독/ 배우의 스타성과 장르및 기타 요소들을 이용하여
ML을 통한 흥행요소 예측을 통한 스크린 

## 작동환경
* OS : Windows 10

* 언어 : Python 3.6

* 개발환경 : jupyter notebook

* 사용 라이브러리 : Pandas, Sklearn, numpy, matplotlib, os, glob, json, selenum

## 정보수집사이트 
               
               https://www.naver.com
               https://www.daum.net/
               http://www.kobis.or.kr/kobisopenapi/homepg/apiservice/searchServiceInfo.do
               http://www.kobis.or.kr/kobis/business/mast/mvie/searchMovieList.do
 
 ## 프로그램 개요 및 진행방향
 
 * 개요 : 영화산업의 핵심은 스크린 편성인데 그 편성과정을 좀더 정확하고 다양한 요소들을 검증하여 사용할수 있는 분석을 하여 검증할수 있는           도구를 만들려고함 최근 WB에서도 AI도입을 결정하였음
 
 * 진행방향 : 데이터 수집 - 전처리 - 분석
 
 ### 데이터 수집
 ---
 
 * 2016년도~2018년도 까지의 개봉작 : KOBIS 사이트의 API를 활용 필요한 자료를 json 및 xml로 받아서 처리
 
 * 총 관람객 및 평점 데이터 : selenum을 활용하여 네이버에서 xPath 를 통한 크롤링
 
 * 감독 & 배우의 출연작 : 다음에서 검색하여 출연작의 관람객 데이터 selenum을 활용한 크롤링
 
 * 1~4주치 별 관람객 : KOBIS 사이트에서 selenum을 통한 검색으로 영화 관람객 일별 데이터 다운로드(자동화)
 
 * 휴일 : 네이버에서 '2016년 공휴일' 이라고 검색하면 나오는 자료를 활용
 
 ### 전처리
 ---
 
 * 일별 관람객 데이터를 주차별 관람객으로 수정후 4주 이상의 상영이 안된영화는 제외
 
 * 감독 & 배우의 출연작풀의 관람객 평균을 감독 및 배우의 스타성 이라고 정의하고 이름을 대신하여 사용
 
 * 장르는 dataframe에 펼쳐서 저장 
        
        ex) 로맨스|판타지|액션
               1     0    1
 
 * 국가 및 나라를 3: 한국 2: 미국 1: 그외 국가로 축소 통일
 
 * 관람연령을 1~4까지 라벨링 하여 사용
 
 * 배급사를 1~3까지 라벨링 하여 사용
 
 * 종속변수 관람객의 클래스를 A,B,C,D로 4등분하여 사용
 
 ### 분석
 ---
 * 가중요소의 분석을 위해서 대표적인 Random Forest 랑 Decision Tree 사용
 
 * Random Forest의 경우 과적합이 일어나는 경우가 많고 가중요소의 다양성이 떨어지는 문제점이 발생함
 * Decision Tree의 경우 과적합이 일어나는 경우가 적고 가중요소의 다양성이 늘어남
 
 #### 이미지 결과
 ---
 * Decision TreeClassifier
 <div>
  <img width="200" src="https://user-images.githubusercontent.com/22620301/80441614-3b126a00-8946-11ea-8248-30d27192d326.png">
  <img width="200" src="https://user-images.githubusercontent.com/22620301/80441620-3cdc2d80-8946-11ea-9e19-68cd20dcb122.png">
  <img width="200" src="https://user-images.githubusercontent.com/22620301/80441623-3d74c400-8946-11ea-9533-523e93fcb4d7.png">
  <img width="200" src="https://user-images.githubusercontent.com/22620301/80441627-3ea5f100-8946-11ea-9407-21d4229dec77.png">
 </div>
 
 * RandomForest Classifier
 <div>
  <img width="200" src="https://user-images.githubusercontent.com/22620301/80441629-3f3e8780-8946-11ea-8be8-ad9fb09d177a.png">
  <img width="200" src="https://user-images.githubusercontent.com/22620301/80441632-3fd71e00-8946-11ea-92d1-cafc17139f4b.png">
  <img width="200" src="https://user-images.githubusercontent.com/22620301/80441636-406fb480-8946-11ea-815b-067851286658.png">
  <img width="200" src="https://user-images.githubusercontent.com/22620301/80441640-41a0e180-8946-11ea-932c-50024a0a1791.png">
 </div>
 
 ### 결론
 ---
 * 1주차 기준 기준 가장 비중이 높은 가중요소 : 감독, 배우, 배급사, 휴일
 
 * 4주차 기준 가장 비중이 높은 가중요소로 : 주차별 관람객 , 감독, 배우, 배급사
 
 * 스크린의 배분은 이전 주차의 실적과 함께 배우 나 감독의 인기도가 중요한것으로 판단될수 있으며 첫주차에는 감독의 지명도와 휴일 같은 요소들을 고려해서 배분하는것이 중요해 


#### 번외(장르만 따로 머신러닝)
---
* 장르(RandomForest)
<div>
  <img width="200" src="https://user-images.githubusercontent.com/22620301/80441631-3f3e8780-8946-11ea-8825-ff0102ec0d4d.png">
  <img width="200" src="https://user-images.githubusercontent.com/22620301/80441634-3fd71e00-8946-11ea-8fe1-d94cdd006562.png">
  <img width="200" src="https://user-images.githubusercontent.com/22620301/80441637-41084b00-8946-11ea-9e09-63e728b56642.png">
  <img width="200" src="https://user-images.githubusercontent.com/22620301/80441642-42397800-8946-11ea-8b06-c51fcba11253.png">
</div>

장르 만을 가지고 머신러닝을 돌려보았을때는 정확도가 낮아지나 액션장르의 경우 데이터의 갯수가 2~3위에 불가하나
영향력이 큰것으로 보아서 액션영화의 인기가 높다고 판단될수도 있다.
  
