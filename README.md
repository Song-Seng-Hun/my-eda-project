# 🎲 보드게임 트렌드 분석 EDA 프로젝트 🎲
## 프로젝트 설명
  - 세계 최대 규모 보드게임 커뮤니티 사이트 BoardGameGeek으로부터 데이터를 추출하여 **EDA를 통한 향후 트렌드**를 분석하는 프로젝트

## 목표
![image](https://user-images.githubusercontent.com/69943723/218906164-746f8bbb-169d-497a-a320-1e83f9fd1697.png)  
탐색적 데이터 분석을 통해 다양한 관점에서 보드게임의 현재까지의 트렌드를 분석하여 **향후 보드게임 산업의 방향을 예측, 제안**해보자 한다.

## 결론
![image](https://user-images.githubusercontent.com/69943723/218908375-8ff06a7d-17d9-4633-b3f4-03c23e8a7a10.png)  
![image](https://user-images.githubusercontent.com/69943723/218908392-a6804c99-8ab5-4dc6-bd77-a37c3855cc5c.png)  
![image](https://user-images.githubusercontent.com/69943723/218908430-f37d0c34-be45-4ada-91d8-2b9070a9ff19.png)  
배경 시대, ip 매체, 구성물, 권장연령, 권장인원, 최대플레이시간, 가격 등 **여러가지 측면에서 데이터들을 분석**해본 결과 **유의미해보이는 경향성**을 얻어낼 수 있었다.

## 주제 선정 배경
  1. 보드게임이라는 분야가 사람들에게 생소한 분야이기에 신선한 시도를 하기에 좋은 주제라고 판단.
  2. 국내외 보드게임 커뮤니티 사이트에 데이터가 매우 잘 정리되어 있어 분석을 위한 데이터를 모으기 용이했다.
  3. 방대한 양의 데이터를 다뤄보는 경험을 체험해보기 위한 목적
  4. 특정 산업 분야의 트렌드를 분석하는 주제이기에 실무적으로도 의의가 있을 것으로 판단.

## 크롤링
**출처 사이트**
- [보드게임긱](https://boardgamegeek.com/) : 세계 최대의 보드게임 커뮤니티 사이트, 해외 보드게임 트렌드 분석을 위한 자료를 수집하는데 사용하였다.  
- [보드라이프](https://boardlife.co.kr/) : 국내 최대의 보드게임 커뮤니티 사이트, 국내 보드게임 트렌드 분석을 위한 자료를 수집하는데 사용하였다.  
- [다나와](https://www.danawa.com/) : 가격비교 사이트, 다른 항목 상품들과의 비교를 위해 사용하였다.  
해당 보드게임 사이트들은 마니악한 보드게임을 고평가하고 캐주얼한 파티게임을 저평가하는 경향성이 있기에 약간의 편향성이 존재할 수 있다는 한계가 있을 수 있다.  
![image](https://user-images.githubusercontent.com/69943723/218630454-c1df86fb-af02-4703-9e4c-1525b915fa16.png)  
![image](https://user-images.githubusercontent.com/69943723/218630391-dd95b69f-80a7-4693-8ad2-e7ef474d7586.png)  

**[출처 사이트 구조]**   
표 형식으로 구성된 목록에 랭킹, 이름, 발매년도, 점수, 가격 등의 점수가 정리되어 있다.  
해당 항목 클릭 시 상세페이지로 연결되어 권장연령, 난이도, 예상플레이시간, 카테고리, 매커니즘 등 추가적인 정보를 수집할 수 있다.  

![image](https://user-images.githubusercontent.com/69943723/218630720-f15006d5-e798-491a-a9cc-941e6219dd6b.png)  
**난점1.** : 다루는 데이터의 양이 방대해 코드가 무거워지고 프로그램이 처리하는데 시간이 오래 걸렸다.  
총 38만개의 데이터 중 유저 평가가 존재하는 상위 23900개의 데이터만을 수집하고 취급했다.  

![image](https://user-images.githubusercontent.com/69943723/218630734-6544e07b-12b0-417f-86ed-febea9805c44.png)  
**난점2** : 사이트에서 데이터 목록의 특정구간(20번 이상의 항목)을 조회하기 위해서는 로그인 되어있을 것을 요구했다.  
Selenium으로 로그인 한 뒤, 쿠키 정보를 저장해. 해당 쿠키 정보를 가지고 있는 세션을 통해 BeautifulSoup으로 크롤링하는 것이 가능했다.  

![image](https://user-images.githubusercontent.com/69943723/218630747-bb91bd93-2b2b-4384-9a5a-146d1183c09d.png)  
![image](https://user-images.githubusercontent.com/69943723/218630756-b48fb2d4-4a8e-464e-a05f-4379fc305918.png)  
**난점3** : 수집한 soup 상에서 원하는 정보를 조회해봤더니 해당 정보가 존재하지 않는다는 결과가 나왔다.  
이는 해당 사이트가 javaScript를 통해 화면 구성이 이루어지는 동적 페이지였기에 발생하는 문제였으며, javaScript 상에 존재하는 문자를 정규식을 통해 정리해 원하는 데이터들을 수집하는 것이 가능했다.  

![image](https://user-images.githubusercontent.com/69943723/218630769-36fcac7a-3709-458c-bb02-530071451832.png)  
**난점4** : 국내 사이트에서 대량의 데이터를 수집하려 시도했더니, 해당 사이트에서 접속을 차단하여 수집이 불가능했다.  
따라서 국내 사이트를 출처로 하는 데이터는 상위 100개의 데이터만 수집하고 다루기로 했다.  

![image](https://user-images.githubusercontent.com/69943723/218630787-445c1a1b-6a8b-4c98-b8c3-62886582f3a8.png)  
**난점5** : 다루고자 하는 데이터의 카테고리, 매커니즘의 종류수가 굉장히 많았으며, 하나의 항목에 대응되는 카테고리, 매커니즘의 수가 1개가 아니었다.(1:1대응이 아니다.)  
여러개의 카테고리, 매커니즘을 나타내는 String들을 List 형태처럼 구성해서 하나의 행에 넣어, 사용할 때에는 별개의 함수를 만들어 처리했다.  

## 데이터 프레임 가공
![image](https://user-images.githubusercontent.com/69943723/218619754-172d5527-52eb-43c3-b17f-f9b1a9f1c7b0.png)  
각 보드게임 항목별 존재하는 데이터프레임을 선그래프로 분석하기 위해 발매년도를 기준으로 groupby를 통해 통합을 하여 년도별 발매량 데이터프레임으로 가공하였다.  
이후 절대적인 양이 아닌 상대적인 비율을 보기 위해 최대값을 1로 scaling하는 함수를 만들었으며 해당하는 데이터프레임으로 가공하였다.  

![image](https://user-images.githubusercontent.com/69943723/218629585-a0209995-07d3-4303-b9b5-672dfc7d32fa.png)  
다루는 매커니즘 수가 과도하게 많아 이를 분석하기 위해 매커니증이 정의되어있는 해당 사이트의 공식문서를 보고 비슷한 매커니즘끼리 통합하여 다루었다. 
통합하는 기준에 주관이 개입되었을 여지가 있다는 한계가 있을 수 있다.  

## 시각화 및 데이터 분석
시각화를 통한 데이터 분석은 크게 발매년도별 발매량 절대값을 분석하기 위한 **꺾은선그래프**, 실제 일어난 역사적 사건과 발매량의 변화를 비교해 보기 위한 **움직이는 바 그래프**, 발매년도에 따른 발매비율의 변화를 분석하기 위한 **누적바그래프**, 전체적인 비율을 보기 위한 **파이그래프**로 구성된다.  
꺾은 선 그래프는 년도에 따라 어떻게 발매량이 급증했는가 보여주기 용이하지만, 항목이 많아질 경우 상세한 분석이 어려워진다는 단점이 존재한다. 
움직이는 바 그래프의 경우, 실제 역사적 상황과 비교해 영향을 끼친 요인을 찾아내기에 용이하지만, 전체적으로 흐름이 어떻게 변했는지 한 눈에 파악하기엔 부적합하다는 단점이 존재한다.  
누적 바 그래프의 경우, 전체 시간 상에서 각 비율이 어떻게 변화하는지 한 눈에 파악하기에 용이하지만, 왼쪽과 오른쪽 그래프의 데이터 양에 차이가 크기 떄문에 비율상으로는 감소하나 절대값 상으로는 증가하는 등의 케이스가 존재해 해석에 오류를 가져올 수 있다는 한계점이 존재한다.  
파이그래프의 경우 전체 비율 구성을 파악기에 용이하나 전체 시간상에서의 통합 비율이 해당 통계를 대표하는 값으로 적합한가하는 문제가 있다.  

### 상관관계 분석
![Screenshot from 2023-02-14 11-49-29](https://user-images.githubusercontent.com/69943723/218626290-80e5afd1-f445-4fa0-a83a-2c2b8e64859e.png)  
우선 간단한 상관관계를 출력해보았다.
주목할 만한 상관관계로는 다음과 같은 것들이 있었다.
- **난이도**와 **평점**이 강한 상관관계를 보였다. 사람들은 쉬운 게임보다 어려운 게임을 선호한다고 분석할 수 있겠다.
- **권장 연령**과 **난이도** 역시 강한 상관관계를 보였다. 이에 따라 자연스럽게 **권장 연령**과 **평점** 역시 상관관계가 나타났다.
- **평점**과 **가격**은 약한 상관관계를 보였다. 이에 따라 **난이도**와 **가격**역시 상관관계를 띄게 되었다.
- **출시일**이 경과함에 따라 약하지만 **평점**이 올라가는 점도 흥미로웠다.
### 배경 시대별 분석
![1](https://user-images.githubusercontent.com/69943723/218626628-71144b2a-4013-4728-a7f5-4945147daf4b.png)  
![image](https://user-images.githubusercontent.com/69943723/218626750-1ae9fca3-45b8-4a5f-885c-4c0f17f91298.png)  
![image](https://user-images.githubusercontent.com/69943723/218628931-37270f6f-b05e-4a8e-b43d-695d157a4f2e.png)  
![image](https://user-images.githubusercontent.com/69943723/218626844-4c7d27dd-dfbb-4fcc-999e-867d1f368cb1.png)  
![image](https://user-images.githubusercontent.com/69943723/218626991-1312accf-e25c-42ed-b2ca-9ae20aee19fe.png)  
### 매체별 분석
![image](https://user-images.githubusercontent.com/69943723/218628769-10d2c79c-9a6f-4ec6-a0b5-f15557fff1a6.png)  
![image](https://user-images.githubusercontent.com/69943723/218629284-30cf3cb5-7096-40b9-8898-93b69942adf9.png)  
![image](https://user-images.githubusercontent.com/69943723/218628808-0f05dd02-523a-4ca4-a3c0-cedffd4fd207.png)  
![image](https://user-images.githubusercontent.com/69943723/218628827-26f4ffa7-ee30-4300-836f-0357e015f84a.png)  
### 테마별 분석
![image](https://user-images.githubusercontent.com/69943723/218629317-4484a5c5-da9b-4f89-aeba-d0e7a3398810.png)  
![image](https://user-images.githubusercontent.com/69943723/218629347-1cd7df13-8c7e-4c39-a0a4-c79421246528.png)  
![image](https://user-images.githubusercontent.com/69943723/218629369-6e2640a6-b2ca-474a-9f83-fb5a796d5802.png)  
![image](https://user-images.githubusercontent.com/69943723/218629387-8259eccc-3007-4b8d-bb2e-377c64c60530.png)  
### 구성물별 분석
![image](https://user-images.githubusercontent.com/69943723/218629446-607debec-38e2-49e0-800b-c5d4da2b9825.png)  
![image](https://user-images.githubusercontent.com/69943723/218629467-ca93405d-0c3e-4257-8843-f59c5c398bb6.png)  
![image](https://user-images.githubusercontent.com/69943723/218629476-4a6ad435-432d-4efe-935f-def6256094aa.png)  
### 도메인 분야별 분석
![image](https://user-images.githubusercontent.com/69943723/218629491-92c5903b-53f0-4a92-adc1-cc6ed4697809.png)  
![image](https://user-images.githubusercontent.com/69943723/218629522-b52244c0-894d-42d9-8208-e8a2e3f8d7ff.png)  
![image](https://user-images.githubusercontent.com/69943723/218629550-bb1923d1-4a8a-4d66-b1b2-b23315a75af7.png)  
![image](https://user-images.githubusercontent.com/69943723/218629562-7423ef49-dc6c-490d-9b14-60a5bea11659.png)  
### 게임 매커니즘별 분석
![image](https://user-images.githubusercontent.com/69943723/218629611-a2f72028-dece-4f8d-81f9-4617bf82a868.png)  
![image](https://user-images.githubusercontent.com/69943723/218629627-9a8cf636-4364-43e7-be6a-c05117d2299e.png)  
![image](https://user-images.githubusercontent.com/69943723/218629747-ffc3ec41-30f2-427e-a1ba-6c34b6ce9941.png)  
![image](https://user-images.githubusercontent.com/69943723/218629757-cc00a465-2581-44aa-b1da-79c0af9d7ed3.png)  
### 권장 최소연령별 분석
![image](https://user-images.githubusercontent.com/69943723/218629781-14695603-c274-4bf1-b5eb-a2251daaca3e.png)  
![image](https://user-images.githubusercontent.com/69943723/218629795-b59af133-bce5-4dcd-99aa-0ce680cb4176.png)  
![image](https://user-images.githubusercontent.com/69943723/218629805-346064ec-9075-4cd4-b771-0e0c0cdb7a89.png)  
### 게임 복잡도별 분석
![image](https://user-images.githubusercontent.com/69943723/218629820-20d0e0bf-1b58-4538-8309-4cabed169801.png)  
![image](https://user-images.githubusercontent.com/69943723/218629839-c16fc9fe-e4bd-4b39-8b60-c0c043280b96.png)  
![image](https://user-images.githubusercontent.com/69943723/218629853-2878b17b-3133-406d-8aa7-bc4745da73f0.png)  
### 권장 최소인원별 분석  
![image](https://user-images.githubusercontent.com/69943723/218629868-d3cebbbc-afc3-44f8-bb41-6326dde8f00f.png)  
![image](https://user-images.githubusercontent.com/69943723/218629881-00fed89e-33b7-4b59-92c7-5c1dc54a42f5.png)  
![image](https://user-images.githubusercontent.com/69943723/218629894-b3955433-6107-4afd-83cf-d21a2ca57bef.png)  
### 게임 최대 플레이시간별 분석
![image](https://user-images.githubusercontent.com/69943723/218629911-3880a342-4857-4351-a9f4-23928a9967b1.png)  
![image](https://user-images.githubusercontent.com/69943723/218629923-034bc2e7-9f0d-4a7a-a216-9686978880c8.png)  
![image](https://user-images.githubusercontent.com/69943723/218629941-db3c6834-f641-4bb0-a44e-585215184d98.png)  
### 가격 분석  
![image](https://user-images.githubusercontent.com/69943723/218629965-b9e9fff5-3406-4942-9f49-b2b36a8aa6a3.png)  
![image](https://user-images.githubusercontent.com/69943723/218629972-a69edafe-52af-4421-a363-29b66595f98a.png)  
![image](https://user-images.githubusercontent.com/69943723/218629980-5a08a440-dc49-4838-9715-f4c6fc3a25c6.png)  
![image](https://user-images.githubusercontent.com/69943723/218629989-d780029e-f034-44fc-b05a-0e02f51947be.png)  
![image](https://user-images.githubusercontent.com/69943723/218629997-b4aed981-81b6-49ea-aa56-29822796a990.png)  
## 유추되는 미래 경향성
- 시간의 흐름에 따라 SF 분야의 수요가 늘어나는 것으로 보이나, 사람들은 낯선 주제를 선호하는 것으로 보인다.  따라서 마찬가지로 시간에 따라 수요가 늘어나는 경향을 보이는 중세 배경 판타지 장르를 배경으로 삼는 것이 주류일 것으로 예상된다.
- 지금까지의 추세로 보았을 때, 특히 코로나 등의 여파가 남아있다면 더더욱 1인용 플레이를 지원하는 보드게임이 강세일 것으로 예상된다.
- 시간의 흐름에 따라 전체적으로 게임의 난이도가 높아지는 경향이 보인다. 따라서 플레이 시간이 길고 복잡한 구성도 시장에서 받아들여질 것으로 예상된다.
- 현대로 넘어올수록 만화, 게임을 원작으로 하는 보드게임이 늘어나는 것을 볼 때 여러 게임, 만화의 판권
## 아쉬운 점..
- 발매 국가 등에 대한 데이터가 존재하지 않아 국가별 통계 분석이 불가능하였다.
- 국내산 보드게임이 유의미한 정도의 규모가 아니기 때문에 국내산 보드게임에 대한 분석을 할 수 없었다.
- 해당 데이터로 알 수 있는 것은 발매종류뿐, 실질적인 판매량에 대한 데이터는 알 수 없다. 따라서 많이 발매되는 분야에 대한 분석은 가능하나 많이 판매되는 분야는 알기 어렵다.
- 국내 발매후 해외가격 대비 국내가격에 대한 데이터 역시 얻을 수 없었다.  

시간이 더 있었다면..  
- 움직이는 바 그래프의 항목별 아이콘 이미지가 표시되게끔 만들고 싶었다.
- 움직이는 바 그래프에 좀 더 다양하고 정확한 역사 연표를 표기하고 싶었다.
- 파이그래프도 막대그래프처럼 움직이는 시각화를 시도해보고 싶었다.
- 부족한 데이터를 얻기 위해 국내 사이트를 좀 더 조사해보고 싶었다.
## 팀원
  - [성용호](https://github.com/yongho0166) : 웹 크롤링, 데이터 수집 담당 (사용툴 : Selenium, BeautifulSoup, pandas)
  - [송승훈](https://github.com/Song-Seng-Hun) : 데이터 프레임 전처리, 가공 담당 (사용툴 : pandas, numpy, matplotlib)
  - [신재성](https://github.com/JaeseongShin) : 시각화, 디자인 담당 (사용툴 : pandas, matplotlib)
## 첨부 데이터
- 크롤링
  - data_crawl.ipynb (성용호) : BoardGameGeek 사이트에서 크롤링을 통한 데이터 추출하는 코드
  - danawa.ipynb (신재성) : 다나와 사이트에서 아동용 장난감 가격 데이터를 추출하는 코드
  - danawa_golf.ipynb (신재성) : 다나와 사이트에서 골프용품 가격 데이터를 추출하는 코드
  - boardlife_df.ipynb (성용호) : 보드라이프로부터 크롤링을 통해 데이터를 추출해서 BoardGameGeek의 데이터와 비교하는 코드
- 데이터 프레임 가공
  - df_preprocessing.ipynb (송승훈) : 크롤링한 데이터들을 1차 전처리해서 사용하기 용이하게 합쳐놓
  - boardgamegeek_df.ipynb (송승훈) :  BoardGameGeek 사이트로부터 추출한 데이터 파일을 가공해서 여러가지 형태로 분석시킨 코드
- 시각화 및 데이터 분석
  - design_graph.ipynb(신재성) : 산출된 그래프를 더 효과적인 시각화가 되도록 디자인 개선시킨 코드
- 데이터
  - [EDA 프로젝트 4조.pptx](https://docs.google.com/presentation/d/1Jpa3Q-Jw3U8QfQBKJXx9b5tj16xVT1cg/edit?usp=sharing&ouid=104392179046615871789&rtpof=true&sd=true) : 프로젝트 발표 pptx
  - [boardgame_df.csv](https://docs.google.com/spreadsheets/d/1of4LKgRJSekfG7D7MoW_KL99-QCkCMQ1V7dfKt4_dZI/edit?usp=sharing) : BoardGameGeek으로 부터 추출한 데이터 csv
  - [booardlife_top100_df](https://docs.google.com/spreadsheets/d/1W933Z1F2266UpCbIoNf2Y9CQXkU7nGX28ZwvIETtjxk/edit?usp=sharing) : Boardlife에서 추출한 상위 100개 보드게임 데이터 csv
