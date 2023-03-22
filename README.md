# Customs-Notification-Analysis-and-Monitoring-System
세관 고시 분석 및 모니터링 시스템  

<br>

## Notice 
본 프로젝트는 현재 KOTRA 내부 서비스 적용을 위해 계약을 진행하였고, 코드를 포함한 최종 결과물의 사용 권한을 KOTRA에 이관하였습니다.   
그렇기에 해당 repository에서는 샘플 데이터, 회의록 등의 일부 자료만 확인 가능합니다.

<br>

## Tech Stacks
![DJANGO](https://img.shields.io/badge/Django-092E20?style=for-the-badge&logo=django&logoColor=green)
![SELENIUM](https://img.shields.io/badge/Selenium-43B02A?style=for-the-badge&logo=Selenium&logoColor=white)
![SQLITE3](https://camo.githubusercontent.com/352d24bbcae518863354f723e8edf6b10b2e1e4bf8a6a7c0b3f5777f3579d249/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f73716c697465332d3030353939433f7374796c653d666f722d7468652d6261646765266c6f676f3d73716c697465266c6f676f436f6c6f723d7768697465)
![GOOGLE CLOUD](https://img.shields.io/badge/Google_Cloud-4285F4?style=for-the-badge&logo=google-cloud&logoColor=white)

<br>

## Collaborative Organization
<img src = "https://user-images.githubusercontent.com/45115733/210560053-353dd44e-1442-4d00-8b92-c62ef2f4e621.png" width = "100" height = "50"/> <img src = "https://user-images.githubusercontent.com/45115733/210559728-81d83fb3-f73c-4757-8d4f-8f5f382de852.PNG" width = "130" height = "40"/>
1. **KOTRA(대한무역투자진흥공사)** - 프로젝트 멘토링, 고도화 진행
2. **BigLeader(빅리더)** - 프로젝트 주관, 협조 진행

<br>

## Project Members
- **Team Leader**
    - [KwanJung98(82KJ)](https://github.com/82KJ/) - FE / BE / Design Auto Scraper / NLP Model Selection & Application
- **Team Members**
  - [JangHyun Noh(NohJangHyun)](https://github.com/NohJangHyun) - Scraping(Japan) / Data Preprocessing / Testing & Results Analysis
  - [Yoona PARK(gyunnas)](https://github.com/gyunnas) - Scraping(America, Australia) / Data Preprocessing / BE
  - [Han_Jinseo(jinseoyaaa)](https://github.com/jinseoyaaa) - Scraping(Vietnam, China) / Data Preprocessing / Testing & Results Analysis

<br>

## Summary
본 시스템은 2021년 10월경 발생한 **요소수 대란**과 같은 **글로벌 공급망 불안 사태를 예방**하기 위해 고안되었다.  
**해외 관세청 세관 고시를 신속하게 파악**하여 **산업 관계자에게 제공**하는 것을 목표로 한다.  
이를 위해 KOTRA(대한무역투자진흥공사)와 연계하여 각종 해결책 및 시스템 구성 방식을 구상하였다.
1. 해외 관세청에 올라오는 세관 고시의 신속한 파악 -> 세관 고시를 매일 크롤링하여 DB에 저장하는 **자동화 시스템** 구축
2. 각 세관 고시가 어떤 품목과 관련되어 있는지 분석 -> NLP 모델을 활용한 문서 **키워드 추출** 방식 적용
3. 각 세관 고시가 대한민국에 어떤 영향을 미칠 수 있는지 파악 -> 문서 키워드와 자체 선정 **모니터링 품목** 매칭 및 **산업군 매칭표** 제공
4. 다양한 산업 관계자를 대상으로 하는 서비스 제공 -> 사용자 친화적이고 직관적인 **웹 서비스** 구현

<br>

## Dataset
1. **5개국 세관 고시 데이터**  
각 국가별 관세청 사이트에 업로드된 세관 고시 수집(날짜, 제목, 링크, 내용, 영어 번역본, 한국어 번역본)
    |국가  |기간                   |개수 |
    |:----:|:--------------------:|:---:|
    |[중국](http://www.customs.gov.cn/customs/302249/302266/index.html)  |1999.11.02~2022.07.25 |2191개|
    |[미국](https://www.cbp.gov/trade/rulings/bulletin-decisions)  |2003.06.18~2022.07.26 |937개 |
    |[일본](https://www.meti.go.jp/policy/external_economy/trade_control/wnlist.html)  |2019.05.29~2022.08.01 |500개 |
    |[호주](https://www.abf.gov.au/help-and-support/notices/australian-customs-notices)  |2018.12.10~2022.08.23 |1620개|
    |[베트남](https://www.customs.gov.vn/index.jsp?pageId=4&cid=30)|2010.08.10~2022.07.01 |1000개|

<br>

2. **모니터링 품목 데이터**  
대한민국과 각 국가 간 교역 품목을 기준으로 모니터링 품목 선정 및 수집(MTI, HSCODE, KSIC)  
    |국가  |대분류|소분류|
    |:----:|:---:|:----:|
    |중국  |100개 |330개 |
    |미국  |100개 |282개 |
    |일본  |100개 |274개 |
    |호주  |100개 |211개 |
    |베트남|100개 |301개 |

<br>

## NLP Model Selection
**Sentence BERT(all-mpnet-base-v2)**  
- 2018년 구글에서 공개한 Pretrained Model인 BERT를 미세 조정하여 **Sentence Embedding의 성능을 극대화**한 모델  
- 다양한 SBERT 모델 중 **Sentence Embeddings와 Semantic의 평균 성능이 가장 뛰어난 all-mpnet-base-v2** 선정  
- 미세 조정을 위해 **10억개의 문장 쌍 데이터로 contrastive learning** 진행    

|Name   |Avg Performance   |Encoding Speed<br>(sentences/sec)   |Size<br>(MB)   |
|:---:|:---:|:---:|:---:|
|all-mpnet-base-v2   |63.30   |2800   |420   |

<br>

## Output View
1. **Dashboard Page**
![Dashboard Page](https://user-images.githubusercontent.com/45115733/210954453-e899fc53-77d2-4722-afba-c5d7db93fbdb.png)  
- **L0 : Scraping Progress Time** - 자동화 시스템 동작으로 DB 갱신 시작
- **L1 : Search Keyword** - 키워드 검색 및 국가별 최신 키워드 출력
- **L2 : Keyword Bar Chart** - 국가별 키워드 비중 막대 그래프
- **L3 : Keyword Table** - 키워드 관련 코드표
- **L4 : Key Customs Notice**- 키워드 관련 국가별 세관 고시
- **L5 : New Customs Notice** - DB 갱신 직후 최신 세관 고시

<br>

2. **Customs Notice Page - Australia**
![Australia1](https://user-images.githubusercontent.com/45115733/210954941-bd4df17d-f5b2-498f-866d-067b81f4fc88.png)  
- **L1 : Key Customs Notice** - 모니터링 품목과 매칭된 핵심 세관 고시 리스트(Date, Title, Keyword, Link)
- **L2 : New Customs Notice** - 최신 세관 고시 리스트(Date, Title, Tag, Link) 

<br>

![Australia2](https://user-images.githubusercontent.com/45115733/210953210-c1ac3041-1215-49b8-9f41-ae08b826df5b.png)   
- **L1 : Matching Table** - 고시 키워드와 국가별 모니터링 품목 매칭표(Keyword, MTI4, MTI6, HSCODE, Industry, More)   

<br>

![Australia3](https://user-images.githubusercontent.com/45115733/210953904-c4baca29-b7ba-4cfa-aa7e-3662821945d9.png)    
- **L1 : More Info Modal** - 모니터링 품목 관련 추가적인 HSCODE, KSIC 리스트  

<br>

1. **Customs Notice Page - China, America, Japan, Vietnam**   
![Country](https://user-images.githubusercontent.com/45115733/210955184-bc5e8ac8-36cd-468b-a43d-7b720b7c8d05.png)    

<br>

**시연 영상 링크**   
<https://www.youtube.com/watch?app=desktop&v=89itkBMtdCQ&feature=youtu.be>