### 당근이 불편했던 이유
1. 유저 위치정보를 기반으로 했기때문에 불편하다.
2. 불필요한 유저의 환승이 필요한 경우가 많았음


#### API에서 뽑아 올 데이터들. 
- 역명
- 호선
- 역 좌표(가장 근접한 역을 찾기 위해)
	- [지하철역 좌표정보(API)](https://t-data.seoul.go.kr/category/dataviewopenapi.do?data_id=1036)
	- *확장성*: 분실물찾기API로 추가 개발 가능

## 사용 api 추리기
- [지하철역 좌표정보(API)](https://t-data.seoul.go.kr/category/dataviewopenapi.do?data_id=1036)

| 변수명       | 타입       | 필수 여부 | 변수 크기 | 변수 설명   | 값 설명 | 샘플데이터   |
| --------- | -------- | ----- | ----- | ------- | ---- | ------- |
| lineNm    | VARCHAR2 |       | 50    | 호선_명칭   |      | 9호선(연장) |
| convX     | NUMBER   |       |       | 환승역_X   |      | 0       |
| stnKrNm   | VARCHAR2 |       | 50    | 역_한글_명칭 |      | 삼성중앙    |
| convY     | NUMBER   |       |       | 환승역_Y   |      | 0       |
| outStnNum | VARCHAR2 |       | 4     | 외구간_역_수 |      | 4128    |


---
https://lab.odsay.com/application/info
API: Dn5+JHyM28NrMZm17U8K3s4lmksWq1h/ty0TOZxhsdg



---

#### **1. 서울특별시_지하철 실시간 도착정보 API**
- 실시간으로 각 지하철역에 열차가 언제 도착하는지 정보 제공
- 중고거래 약속 시간 조율, 역 도착 알림 등에 활용 가능
- 제공 데이터: 역명, 열차 도착 예정 시각, 열차 번호 등
- 출처 
  [공공데이터포털:서울특별시_지하철 실시간 도착정보](https://www.data.go.kr/data/15058052/openapi.do)
  [서울열린데이터광장](https://data.seoul.go.kr/dataList/OA-12764/F/1/datasetView.do)

#### **2. 서울교통공사_==노선별 지하철역 ==정보 API**
- 1~9호선(일부 구간)까지 각 노선별 역 목록 제공
- 거래장소 제안, 역 기반 검색 기능에 활용
- 제공 데이터: 노선명, 역명, 역 코드 등
- 출처 
  [서울교통공사](https://www.data.go.kr/data/15058404/openapi.do)

#### **3. 서울교통공사_ ==역명== 지하철역 검색 API**
- 역명, 역코드, 호선 등으로 지하철역 검색 가능
- 거래장소 자동완성, 역 검색 기능에 적합
- 출처
  [서울교통공사](https://www.data.go.kr/data/15057719/openapi.do)

#### **4. 지하철역 ==좌표정보(API)**==
- 각 지하철역의 위도, 경도 등 위치 정보 제공
- 지도 기반 거래장소 표시, 역간 거리 산출 등에 활용
- 제공 데이터: 역명, 위경도, 환승역 여부 등
- 출처
  [서울교통빅데이터](https://t-data.seoul.go.kr/category/dataviewopenapi.do?data_id=1036)

#### **5. 국토교통부_(TAGO)_지하철정보 API**
- 전국 지하철역 목록, 출구 목록, 출구별 버스노선, 역별 시간표 등 제공
- 서울 외 수도권 및 지방 지하철 포함, 다양한 ==교통 연계== 서비스 가능
- 제공 데이터: 역 목록, 출구 정보, 시간표 등
- 출처: 
  [국토교통부](https://www.data.go.kr/data/15098554/openapi.do)

#### **6. 전국 지하철 노선 전체 정보 오픈 API (철도 데이터 포털)**
- 수도권, 부산, 대구, 광주, 대전 등 전국 주요 도시 지하철의 노선, 역 정보 제공
- 노선별 색상 코드, 권역 정보 등 포함
- 출처:
  [티스토리 활용법](https://chuun92.tistory.com/63)
  [네이버 글로그](https://blog.naver.com/yug311861/221965786543)



## 필요 테이블
1. 회원
2. 중고물품
3. 물품번호카테고리
4. 사진 및 동영상 테이블
5. 채팅
6. 채팅방 목록
7. 댓글테이블(정보성) -foeginkey: 물품테이블
8. 역노선 
##### 테이블 구조
[ERDCloud](https://www.erdcloud.com/d/gMWFgvvawcCZYK2RK)
![[Pasted image 20250526073954.png]]