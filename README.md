# Customs-Notification-Analysis-and-Monitoring-System
세관 고시 분석 및 모니터링 시스템  

<br>

## Notice 
본 프로젝트는 현재 Kotra 내부 서비스 적용을 위해 계약을 진행하였고, 코드를 포함한 최종 결과물의 사용 권한을 Kotra에 이관하였습니다.   
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
- 해외 관세청에 올라오는 세관 고시의 신속한 파악 -> 세관 고시를 매일 크롤링하여 DB에 저장하는 **자동화 시스템** 구축
- 각 세관 고시가 어떤 품목과 관련되어 있는지 분석 -> NLP 모델을 활용한 문서 **키워드 추출** 방식 적용
- 각 세관 고시가 대한민국에 어떤 영향을 미칠 수 있는지 파악 -> 문서 키워드와 자체 선정 **모니터링 품목** 매칭 및 **산업군 매칭표** 제공
- 다양한 산업 관계자를 대상으로 하는 서비스 제공 -> 사용자 친화적이고 직관적인 **웹 서비스** 구현

<br>

## Dataset
1. 5개국 세관 고시 데이터  
각 국가별 관세청 사이트에 업로드된 세관 고시 수집(날짜, 제목, 링크, 내용, 영어 번역본, 한국어 번역본)
    |국가  |기간                   |개수 |
    |:----:|:--------------------:|:---:|
    |중국  |1999.11.02~2022.07.25 |2191개|
    |미국  |2003.06.18~2022.07.26 |937개 |
    |일본  |2019.05.29~2022.08.01 |500개 |
    |호주  |2018.12.10~2022.08.23 |1620개|
    |베트남|2010.08.10~2022.07.01 |1000개|
2. 모니터링 품목 데이터  
대한민국과 각 국가 간 교역 품목을 기준으로 모니터링 품목 선정 및 수집(MTI, HSCODE, KSIC)  
    |국가  |대분류|소분류|
    |:----:|:---:|:----:|
    |중국  |100개 |330개 |
    |미국  |100개 |282개 |
    |일본  |100개 |274개 |
    |호주  |100개 |211개 |
    |베트남|100개 |301개 |